
#include <stdio.h>
#define salary 30000.0

   

struct note {
    char product[80];
    float expenditure;
};

float balance(struct note *product, int numberofproducts) {
    float totalexpenditure = 0.0;

    for (int i = 0; i < numberofproducts; i++) {
        totalexpenditure += product[i].expenditure;
    }

    return (salary - totalexpenditure); 
}

void display(struct note *product, int numberofproducts) {
    if (numberofproducts == 0) {
        printf("No products recorded.\n");
        return;
    }

    float running_balance = salary;
    printf("\nExpense Details:\n\n");

    for (int i = 0; i < numberofproducts; i++) {
        running_balance -= product[i].expenditure;
        printf("Product: %s :: Expenditure: %.2f :: Bal: %.2f\n",
               product[i].product, product[i].expenditure, running_balance);
    }
}

void insert(struct note *product, int *numberofproducts) {
    int pos;

    printf("Enter the pos (%d): ", *numberofproducts);
    scanf("%d", &pos);

    if (pos < 0 || pos > *numberofproducts) {
        printf("Invalid pos.\n");
        return;
    }

    for (int i = *numberofproducts; i > pos; i--) {
        product[i] = product[i - 1];
    }

    (*numberofproducts)++;

    printf("Enter product name: ");
    scanf(" %[^\n]%*c", product[pos].product);

    printf("Enter product expenditure: ");
    scanf("%f", &product[pos].expenditure);

    printf("Balance: %.2f\n", balance(product, *numberofproducts));
}



int main() {
    printf("....................Money Tracker......................\n");
    struct note product[80];
    int choice;
    int numberofproducts = 0;

    while (1) {
        printf("Press 1 to check the salary\n");
        printf("Press 2 to list products with bal\n");
        printf("Press 3 to check total bal\n");
        printf("Press 4 to add a product\n");
        printf("Press 5 to exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Salary: %.2f\n", salary);
                break;
            case 2:
                display(product, numberofproducts);
                break;
            case 3:
                printf("Current bal: %.2f\n", balance(product, numberofproducts));  
                break;
            case 4:
                insert(product, &numberofproducts);
                break;
            case 5:
                printf("Exiting program...\n");
                return 0;
            default:
                printf("Invalid choice.try again.\n");
        }
      }
}

