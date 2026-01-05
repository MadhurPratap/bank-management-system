# bank-management-system
bank management system project report (c programming)

#include <stdio.h>
#include <string.h>

// Structure for a customer account
typedef struct {
    char name[50];
    char accountType[20];
    int accountNumber;
    float balance;
} CustomerAccount;

// Function to create a new account
void createAccount(CustomerAccount *account) {
    printf("Enter customer name: ");
    fgets(account->name, sizeof(account->name), stdin);
    account->name[strcspn(account->name, "\n")] = '\0';

    printf("Enter account type (savings/current): ");
    fgets(account->accountType, sizeof(account->accountType), stdin);
    account->accountType[strcspn(account->accountType, "\n")] = '\0';

    account->accountNumber = 1001;   // Fixed account number
    account->balance = 0.0;          // Initial balance
}

// Function to deposit money
void deposit(CustomerAccount *account, float amount) {
    if (amount > 0) {
        account->balance += amount;
        printf("Deposit successful. New balance: %.2f\n", account->balance);
    } else {
        printf("Invalid deposit amount.\n");
    }
}

// Function to withdraw money
void withdraw(CustomerAccount *account, float amount) {
    if (amount > 0 && amount <= account->balance) {
        account->balance -= amount;
        printf("Withdrawal successful. New balance: %.2f\n", account->balance);
    } else {
        printf("Insufficient balance or invalid amount.\n");
    }
}

// Function to display account details
void displayAccount(CustomerAccount *account) {
    printf("\n----- Account Details -----\n");
    printf("Account Number: %d\n", account->accountNumber);
    printf("Account Holder: %s\n", account->name);
    printf("Account Type: %s\n", account->accountType);
    printf("Balance: %.2f\n", account->balance);
}

int main() {
    CustomerAccount account;
    int choice;
    float amount;

    createAccount(&account);

    while (1) {
        printf("\n--- Bank Management System ---\n");
        printf("1. Deposit\n");
        printf("2. Withdraw\n");
        printf("3. Check Balance\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        getchar(); // clear buffer

        switch (choice) {
            case 1:
                printf("Enter deposit amount: ");
                scanf("%f", &amount);
                deposit(&account, amount);
                break;

            case 2:
                printf("Enter withdrawal amount: ");
                scanf("%f", &amount);
                withdraw(&account, amount);
                break;

            case 3:
                displayAccount(&account);
                break;

            case 4:
                printf("Thank you for using Bank Management System.\n");
                return 0;

            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
}

