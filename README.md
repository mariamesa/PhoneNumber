# PhoneNumber
This program reads in numbers from a file and prints the area code, exchange, and line number for each as well as whether or not the number can be dialed toll free.

import java.util.Scanner;
import java.io.*;

public class PhoneNumber {
    public PhoneNumber (String num) {
       this.number = num;
    }
    public String getAreaCode()  {
        int index1 = number.indexOf("(") + 1;
        int index2 = number.indexOf(")");
        return number.substring(index1, index2);
    }
    public String getExchange () {
        int index1 = number.indexOf("(") + 5;
        int index2 = number.indexOf("-");
        return number.substring(index1,index2);
    }
    public String getLineNumber() {
        int index1 = number.indexOf("-") + 1;
        int index2 = number.indexOf("-") + 5;
        return number.substring(index1,index2);
    }
    public  boolean isTollFree () {
       return number.charAt(1) == '8';
    }
    public static PhoneNumber read (Scanner inFile) {
        if (!inFile.hasNext()) return null;
        String number = inFile.next();
        return new PhoneNumber (number);
    }
    public String toString () {
        return number;
    }
    public boolean equals(PhoneNumber other)  {
        return number.equals(other.number);
    }
    private String number;
    public static void main(String [] arg) throws IOException {
        Scanner inFile = new Scanner(new File("nums.txt"));
        int count = 0;
        PhoneNumber number = read(inFile);
        PhoneNumber duplicate = null;
        while(number != null) {
            if(duplicate == null || number.equals(duplicate)) {
                System.out.println("Duplicate phone number \"" + number.toString() + "\" discovered");
            }
            else {
                System.out.println("phone number: " + number.toString());
                System.out.println("area code: " + number.getAreaCode());
                System.out.println("exchange: " +  number.getExchange());
                System.out.println("line number: " + number.getLineNumber());
                System.out.println("is toll free: " + number.isTollFree());
                System.out.println();
            }
            count++;
            duplicate = number;
            number = read(inFile);
        }
        System.out.println("---");
        System.out.println(count + " phone numbers processed.");
    }
}
