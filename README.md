package numberstats;

import java.util.Scanner;

public class numberstats {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int count = 0;
        int maxNumbers = 5;
        int invalidAttempts = 0;
        int maxInvalidAttempts = 10; // safety break to avoid endless loop
        double total = 0;
        double max = Double.NEGATIVE_INFINITY;
        double min = Double.POSITIVE_INFINITY;

        while (count < maxNumbers) {
            System.out.print("Enter floating-point number (" + (count + 1) + "/" + maxNumbers + "): ");
            if (scanner.hasNextDouble()) {
                double num = scanner.nextDouble();
                total += num;

                if (num > max) max = num;
                if (num < min) min = num;

                count++;
                invalidAttempts = 0; // reset invalid counter after valid input
            } else {
                String bad = scanner.next(); // consume the invalid token
                invalidAttempts++;
                System.out.println("Invalid input \"" + bad + "\". Please enter a number. (" 
                                   + invalidAttempts + "/" + maxInvalidAttempts + " invalid attempts)");
                if (invalidAttempts >= maxInvalidAttempts) {
                    System.out.println("Too many invalid attempts. Exiting program.");
                    scanner.close();
                    return;
                }
            }
        }

        double average = total / maxNumbers;
        double interest = total * 0.20;

        System.out.println("\n--- Results ---");
        System.out.println("Total: " + total);
        System.out.println("Average: " + average);
        System.out.println("Maximum: " + max);
        System.out.println("Minimum: " + min);
        System.out.println("Interest on total at 20%: " + interest);

        scanner.close();
    }
}
