import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class Account {
        private String accountNumber;
        private String pin;
        private double balance;

        public Account(String accountNumber, String pin, double balance) {
                this.accountNumber = accountNumber;
                this.pin = pin;
                this.balance = balance;
        }

        public String getAccountNumber() {
                return accountNumber;
        }

        public boolean validatePin(String pin) {
                return this.pin.equals(pin);
        }

        public double getBalance() {
                return balance;
        }

        public void deposit(double amount) {
                if (amount > 0) {
                        balance += amount;
                        System.out.println("Deposit successful. New balance: ₹" + balance);
                } else {
                        System.out.println("Invalid deposit amount.");
                }
        }

        public void withdraw(double amount) {
                if (amount > 0 && amount <= balance) {
                        balance -= amount;
                        System.out.println("Withdrawal successful. New balance: " + "₹" + balance);
                } else {
                        System.out.println("Invalid withdrawal amount or insufficient funds.");
                }
        }
}

public class Main {
        private Map<String, Account> accounts;
        private Scanner scanner; 

        public Main() {
                accounts = new HashMap<>();
                scanner = new Scanner(System.in);
                // Add some dummy accounts
                accounts.put("123456", new Account("123456", "1234", 500.0));
                accounts.put("654321", new Account("654321", "4321", 1000.0));
                accounts.put("987654" , new Account("987654", "9876", 1500));
                accounts.put("456789" , new Account("456789", "4567", 2000));
        }

        public void start() {
                System.out.println("Welcome to the ATM!");
                System.out.print("Enter your account number: ");
                String accountNumber = scanner.nextLine();
                Account account = accounts.get(accountNumber);

                if (account != null) {
                        System.out.print("Enter your PIN: ");
                        String pin = scanner.nextLine();

                        if (account.validatePin(pin)) {
                                showMenu(account);
                        } else {
                                System.out.println("Invalid PIN.");
                        }
                } else {
                        System.out.println("Account not found.");
                }
        }

        private void showMenu(Account account) {
                int choice;
                do {
                        System.out.println("\nATM Menu:");
                        System.out.println("1. Balance Inquiry");
                        System.out.println("2. Deposit");
                        System.out.println("3. Withdraw");
                        System.out.println("4. Exit");
                        System.out.print("Enter your choice: ");
                        choice = scanner.nextInt();

                        switch (choice) {
                                case 1:
                                        System.out.println("Your balance: ₹" + account.getBalance());
                                        break;
                                case 2:
                                        System.out.print("Enter deposit amount: ");
                                        double depositAmount = scanner.nextDouble();
                                        account.deposit(depositAmount);
                                        break;
                                case 3:
                                        System.out.print("Enter withdrawal amount: ");
                                        double withdrawalAmount = scanner.nextDouble();
                                        account.withdraw(withdrawalAmount);
                                        break;
                                case 4:
                                        System.out.println("Thank you for using the ATM. Goodbye!");
                                        break;
                                default:
                                        System.out.println("Invalid choice. Please try again.");
                        }
                } while (choice != 4);
        }

        public static void main(String[] args) {
                Main atm = new Main();
                atm.start();
        }
}
