import java.util.Scanner;

public class SmartRestaurantOrder {
    public static void main(String[] args) {
        // Constants
        final double DRINK_PRICE = 15.50;
        final double STUDENT_DISCOUNT_RATE = 0.10;
        final double SENIOR_DISCOUNT_RATE = 0.05;
        final double TIP_RATE = 0.10;

        Scanner input = new Scanner(System.in);

        // Collect customer and order information
        System.out.print("Enter customer's name: ");
        String customerName = input.nextLine();

        System.out.print("Enter customer's age: ");
        int age = input.nextInt();

        System.out.print("Enter price of the meal: ");
        double mealPrice = input.nextDouble();

        System.out.print("Enter number of drinks ordered: ");
        int drinkCount = input.nextInt();

        System.out.print("Is the customer a student (true/false)? ");
        boolean isStudent = input.nextBoolean();

        System.out.print("Enter service rating (1 to 5): ");
        int rating = input.nextInt();

        // Validate service rating
        if (rating < 1 || rating > 5) {
            System.out.println("Error: Service rating must be between 1 and 5.");
            input.close();
            return;
        }

        // Calculate costs and subtotal
        double drinksCost = drinkCount * DRINK_PRICE;
        double subtotal = mealPrice + drinksCost;

        // Apply only one discount (the larger one if both qualify)
        double discountRate = 0.0;
        if (isStudent && age >= 60) {
            // Student discount (10%) is larger than senior discount (5%)
            discountRate = STUDENT_DISCOUNT_RATE;
        } else if (isStudent) {
            discountRate = STUDENT_DISCOUNT_RATE;
        } else if (age >= 60) {
            discountRate = SENIOR_DISCOUNT_RATE;
        }

        double discountAmount = subtotal * discountRate;

        // Calculate tip (10% of subtotal when rating is 4 or 5)
        double tipAmount = 0.0;
        if (rating == 4 || rating == 5) {
            tipAmount = subtotal * TIP_RATE;
        }

        // Final bill and whole-number cast
        double finalBill = subtotal - discountAmount + tipAmount;
        int wholeAmount = (int) finalBill;

        // Print receipt
        System.out.println();
        System.out.println("SMART RESTAURANT");
        System.out.println("Customer: " + customerName);
        System.out.printf("Meal: $%.2f%n", mealPrice);
        System.out.printf("Drinks: $%.2f%n", drinksCost);
        System.out.printf("Discount: $%.2f%n", discountAmount);
        System.out.printf("Tip: $%.2f%n", tipAmount);
        System.out.printf("Final bill: $%.2f%n", finalBill);
        System.out.println("Whole amount: $" + wholeAmount);

        input.close();
    }
}
