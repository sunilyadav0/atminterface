import java.util.Scanner;

// Step 1: Create a class to represent the ATM machine
class ATM {
    private BankAccount account;

    // Constructor to initialize ATM with a bank account
    public ATM(BankAccount account) {
        this.account = account;
    }

    // Step 3: Implement methods for each option
    public void withdraw(double amount) {
        if (amount > account.getBalance()) {
            System.out.println("Insufficient balance for withdrawal.");
        } else if (amount <= 0) {
            System.out.println("Invalid withdrawal amount.");
        } else {
            account.withdraw(amount);
            System.out.println("Withdrawal successful. Current balance: $" + account.getBalance());
        }
    }

    public void deposit(double amount) {
        if (amount <= 0) {
            System.out.println("Invalid deposit amount.");
        } else {
            account.deposit(amount);
            System.out.println("Deposit successful. Current balance: $" + account.getBalance());
        }
    }

    public void checkBalance() {
        System.out.println("Current balance: $" + account.getBalance());
    }

    // Step 2: Design the user interface for the ATM
    public void showMenu() {
        Scanner scanner = new Scanner(System.in);
        int choice;
        do {
            System.out.println("ATM Menu:");
            System.out.println("1. Withdraw");
            System.out.println("2. Deposit");
            System.out.println("3. Check Balance");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter the amount to withdraw: ");
                    double withdrawAmount = scanner.nextDouble();
                    withdraw(withdrawAmount);
                    break;
                case 2:
                    System.out.print("Enter the amount to deposit: ");
                    double depositAmount = scanner.nextDouble();
                    deposit(depositAmount);
                    break;
                case 3:
                    checkBalance();
                    break;
                case 4:
                    System.out.println("Thank you for using the ATM. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 4);

        scanner.close();
    }
}

// Step 4: Create a class to represent the user's bank account
class BankAccount {
    private double balance;

    // Constructor to initialize the account with a starting balance
    public BankAccount(double initialBalance) {
        if (initialBalance < 0) {
            this.balance = 0;
        } else {
            this.balance = initialBalance;
        }
    }

    // Methods to access and modify the account balance
    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }
}

// Step 8: The main method to test the ATM interface
public class Main {
    public static void main(String[] args) {
        // Step 6: Create a bank account with an initial balance
        BankAccount account = new BankAccount(1000.00);

        // Create an ATM instance and connect it to the user's bank account
        ATM atm = new ATM(account);

        // Display the ATM menu
        atm.showMenu();
    }
}
