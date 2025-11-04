# dscode

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* link;
};

struct Node* head = NULL;

void insert(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->link = NULL;

    if (head == NULL) {
        head = newNode;
        return;
    }

    struct Node* ptr = head;
    while (ptr->link != NULL)
        ptr = ptr->link;
    ptr->link = newNode;
}

void delete(int value) {
    struct Node *ptr = head, *prev = NULL;

    if (ptr == NULL) {
        printf("List is empty!\n");
        return;
    }

    if (ptr != NULL && ptr->data == value) {
        head = ptr->link;
        free(ptr);
        printf("%d deleted successfully.\n", value);
        return;
    }

    while (ptr != NULL && ptr->data != value) {
        prev = ptr;
        ptr = ptr->link;
    }

    if (ptr == NULL) {
        printf("Value not found!\n");
        return;
    }

    prev->link = ptr->link;
    free(ptr);
    printf("%d deleted successfully.\n", value);
}

void display() {
    struct Node* ptr = head;
    if (ptr == NULL) {
        printf("List is empty!\n");
        return;
    }
    printf("Linked List: ");
    while (ptr != NULL) {
        printf("%d -> ", ptr->data);
        ptr = ptr->link;
    }
    printf("NULL\n");
}

int main() {
    int choice, value;

    while (1) {
        printf("\n--- Singly Linked List Menu ---\n");
        printf("1. Insert\n");
        printf("2. Delete\n");
        printf("3. Display\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
        case 1:
            printf("Enter value to insert: ");
            scanf("%d", &value);
            insert(value);
            break;
        case 2:
            printf("Enter value to delete: ");
            scanf("%d", &value);
            delete(value);
            break;
        case 3:
            display();
            break;
        case 4:
            exit(0);
        default:
            printf("Invalid choice! Please try again.\n");
        }
    }
    return 0;
}
