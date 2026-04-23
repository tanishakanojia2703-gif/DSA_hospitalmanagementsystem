#include <stdio.h>
#include <string.h>

#define MAX 100

struct Patient {
    int id;
    char name[50];
    int age;
    char disease[50];
    int severity; // 1=Critical, 2=Serious, 3=Stable
    char time[10];
};


struct Patient stack[MAX];
int top = -1;


int isEmpty() {
    return top == -1;
}

int isFull() {
    return top == MAX - 1;
}

void admitPatient() {
    if (isFull()) {
        printf("\nER is FULL!\n");
        return;
    }

    struct Patient p;

    printf("\nEnter ID: ");
    scanf("%d", &p.id);

    printf("Enter Name: ");
    scanf(" %[^\n]", p.name);

    printf("Enter Age: ");
    scanf("%d", &p.age);

    printf("Enter Disease: ");
    scanf(" %[^\n]", p.disease);

    printf("Enter Severity (1=Critical, 2=Serious, 3=Stable): ");
    scanf("%d", &p.severity);

    printf("Enter Time (HH:MM): ");
    scanf("%s", p.time);

    stack[++top] = p;

    printf("\nPatient %s admitted successfully!\n", p.name);
}

void dischargePatient() {
    if (isEmpty()) {
        printf("\nNo patients in ER.\n");
        return;
    }

    struct Patient p = stack[top--];

    printf("\nDischarged Patient:\n");
    printf("ID: %d | Name: %s | Severity: %d\n", p.id, p.name, p.severity);
}

void viewTopPatient() {
    if (isEmpty()) {
        printf("\nNo patients available.\n");
        return;
    }

    struct Patient p = stack[top];

    printf("\nMost Recent Patient:\n");
    printf("ID: %d | Name: %s | Age: %d | Disease: %s | Severity: %d | Time: %s\n",
           p.id, p.name, p.age, p.disease, p.severity, p.time);
}

void displayPatients() {
    if (isEmpty()) {
        printf("\nNo patients in ER.\n");
        return;
    }

    printf("\n--- Patient Stack (Top to Bottom) ---\n");

    for (int i = top; i >= 0; i--) {
        printf("\nID: %d | Name: %s | Age: %d | Disease: %s | Severity: %d | Time: %s\n",
               stack[i].id, stack[i].name, stack[i].age,
               stack[i].disease, stack[i].severity, stack[i].time);
    }
}

void searchPatient() {
    if (isEmpty()) {
        printf("\nNo patients available.\n");
        return;
    }

    int id, found = 0;
    printf("\nEnter ID to search: ");
    scanf("%d", &id);

    for (int i = top; i >= 0; i--) {
        if (stack[i].id == id) {
            printf("\nPatient Found:\n");
            printf("ID: %d | Name: %s | Age: %d | Disease: %s | Severity: %d | Time: %s\n",
                   stack[i].id, stack[i].name, stack[i].age,
                   stack[i].disease, stack[i].severity, stack[i].time);
            found = 1;
            break;
        }
    }

    if (!found)
        printf("\nPatient not found.\n");
}

void countPatients() {
    printf("\nTotal Patients: %d\n", top + 1);
}

void stackStatus() {
    printf("\nStack Status:\n");
    printf("Size: %d/%d\n", top + 1, MAX);
    printf("Empty: %s\n", isEmpty() ? "Yes" : "No");
    printf("Full: %s\n", isFull() ? "Yes" : "No");
}

int main() {
    int choice;

    do {
        printf("\n====================================\n");
        printf(" HOSPITAL ER STACK MANAGEMENT SYSTEM\n");
        printf("====================================\n");
        printf("1. Admit Patient\n");
        printf("2. Discharge Patient\n");
        printf("3. View Recent Patient\n");
        printf("4. Display All Patients\n");
        printf("5. Search Patient\n");
        printf("6. Count Patients\n");
        printf("7. Stack Status\n");
        printf("0. Exit\n");
        printf("Enter choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: admitPatient(); break;
            case 2: dischargePatient(); break;
            case 3: viewTopPatient(); break;
            case 4: displayPatients(); break;
            case 5: searchPatient(); break;
            case 6: countPatients(); break;
            case 7: stackStatus(); break;
            case 0: printf("\nExiting...\n"); break;
            default: printf("\nInvalid choice!\n");
        }

    } while (choice != 0);

    return 0;
}
