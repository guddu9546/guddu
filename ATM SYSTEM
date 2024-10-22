import java.util.Scanner;

public class ATM {
    private static double atmBalance = 100000; // Initial ATM balance
    private static double userBalance = 10000; // Initial user account balance

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("ATM Menu:");
            System.out.println("1. Withdraw Money");
            System.out.println("2. Deposit Money");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    withdrawMoney(scanner);
                    break;
                case 2:
                    depositMoney(scanner);
                    break;
                case 3:
                    System.out.println("Exiting...");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 3);

        scanner.close();
    }

    private static void withdrawMoney(Scanner scanner) {
        System.out.print("Enter amount to withdraw: ");
        double amount = scanner.nextDouble();

        if (amount <= 0) {
            System.out.println("Please enter a valid amount greater than zero.");
            return;
        }

        if (amount > atmBalance) {
            System.out.println("ATM does not have enough balance.");
            return;
        }

        if (amount > userBalance) {
            System.out.println("Insufficient account balance.");
            return;
        }

        // If all checks pass
        userBalance -= amount;
        atmBalance -= amount;
        System.out.println("Withdrawal successful! New user balance: " + userBalance);
        System.out.println("New ATM balance: " + atmBalance);
    }

    private static void depositMoney(Scanner scanner) {
        System.out.print("Enter amount to deposit: ");
        double amount = scanner.nextDouble();

        if (amount <= 0) {
            System.out.println("Please enter a valid amount greater than zero.");
            return;
        }

        if (amount > 50000) {
            System.out.println("Maximum deposit amount is 50000.");
            return;
        }

        // If all checks pass
        userBalance += amount;
        atmBalance += amount;
        System.out.println("Deposit successful! New user balance: " + userBalance);
        System.out.println("New ATM balance: " + atmBalance);
    }
}
