import java.util.Scanner;

class Account {
    private String accountNumber;
    private int pin;
    private double balance;

    public Account(String accountNumber, int pin, double balance) {
        this.accountNumber = accountNumber;
        this.pin = pin;
        this.balance = balance;
    }

    public String getAccountNumber() {
        return accountNumber;
    }

    public boolean checkPin(int enteredPin) {
        return this.pin == enteredPin;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        balance += amount;
        System.out.println("Amount Deposited Successfully!");
    }

    public boolean withdraw(double amount) {
        if (amount > balance) {
            return false;
        }
        balance -= amount;
        return true;
    }
}

public class ATM_Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        // Sample account
        Account acc = new Account("1234567890", 1234, 15000.00);

        System.out.println("===== ATM SYSTEM =====");
        System.out.print("Enter Account Number: ");
        String enteredAcc = sc.nextLine();

        System.out.print("Enter PIN: ");
        int enteredPin = sc.nextInt();

        if (!acc.getAccountNumber().equals(enteredAcc) || !acc.checkPin(enteredPin)) {
            System.out.println("Invalid Account Number or PIN!");
            return;
        }

        System.out.println("\nLogin Successful!");
        System.out.println("-------------------------");

        while (true) {
            System.out.println("\nChoose Transaction:");
            System.out.println("1. Balance Inquiry");
            System.out.println("2. Cash Withdrawal");
            System.out.println("3. Cash Deposit");
            System.out.println("4. Exit");
            System.out.print("Enter Choice: ");
            int choice = sc.nextInt();

            switch (choice) {

                case 1:
                    System.out.println("Your Balance: ₹" + acc.getBalance());
                    break;

                case 2:
                    System.out.print("Enter Amount to Withdraw: ");
                    double wAmount = sc.nextDouble();

                    if (acc.withdraw(wAmount)) {
                        System.out.println("Withdrawal Successful!");
                        System.out.println("Remaining Balance: ₹" + acc.getBalance());
                    } else {
                        System.out.println("Insufficient Balance!");
                    }
                    break;

                case 3:
                    System.out.print("Enter Amount to Deposit: ");
                    double dAmount = sc.nextDouble();
                    acc.deposit(dAmount);
                    System.out.println("Updated Balance: ₹" + acc.getBalance());
                    break;

                case 4:
                    System.out.println("Thank You for Using ATM!");
                    System.exit(0);
                    break;

                default:
                    System.out.println("Invalid Option! Try Again.");
            }
        }
    }
}
