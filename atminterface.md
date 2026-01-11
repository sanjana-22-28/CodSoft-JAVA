import java.util.Scanner;

public class atminterface {
    private static final int PIN = 1234; // Hardcoded PIN for simplicity
    private static double balance = 1000.00; // Initial balance

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to the ATM!");

        // Authentication
        System.out.print("Enter your 4-digit PIN: ");
        int enteredPin = scanner.nextInt();
        if (enteredPin != PIN) {
            System.out.println("Invalid PIN. Exiting...");
            return;
        }
        System.out.println("Login successful!");

        // Main menu loop
        boolean running = true;
        while (running) {
            System.out.println("\nATM Menu:");
            System.out.println("1. Check Balance");
            System.out.println("2. Withdraw Money");
            System.out.println("3. Deposit Money");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    checkBalance();
                    break;
                case 2:
                    withdrawMoney(scanner);
                    break;
                case 3:
                    depositMoney(scanner);
                    break;
                case 4:
                    System.out.println("Thank you for using the ATM. Goodbye!");
                    running = false;
                    break;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
        scanner.close();
    }

    private static void checkBalance() {
        System.out.printf("Your current balance is: $%.2f\n", balance);
    }

    private static void withdrawMoney(Scanner scanner) {
        System.out.print("Enter amount to withdraw: $");
        double amount = scanner.nextDouble();
        if (amount > balance) {
            System.out.println("Insufficient funds.");
        } else if (amount <= 0) {
            System.out.println("Invalid amount.");
        } else {
            balance -= amount;
            System.out.printf("Withdrawal successful. New balance: $%.2f\n", balance);
        }
    }

    private static void depositMoney(Scanner scanner) {
        System.out.print("Enter amount to deposit: $");
        double amount = scanner.nextDouble();
        if (amount <= 0) {
            System.out.println("Invalid amount.");
        } else {
            balance += amount;
            System.out.printf("Deposit successful. New balance: $%.2f\n", balance);
        }
    }
}
