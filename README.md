# 3
#include <stdio.h>
#include <string.h>

struct Contact
{
    char name[50];
    char phone[15];
    char email[50];
};

struct Contact contacts[100];
int count = 0;

// Function to add contact
void addContact()
{
    int valid, i;

    if(count >= 100)
    {
        printf("\nContact list is full!\n");
        return;
    }

    printf("\nEnter your name: ");
    scanf(" %49[^\n]", contacts[count].name);

    // Phone number validation
    do
    {
        valid = 1;

        printf("Enter your 10-digit phone number: ");
        scanf("%14s", contacts[count].phone);

        if(strlen(contacts[count].phone) != 10)
        {
            valid = 0;
        }
        else
        {
            for(i = 0; i < 10; i++)
            {
                if(contacts[count].phone[i] < '0' ||
                   contacts[count].phone[i] > '9')
                {
                    valid = 0;
                    break;
                }
            }
        }

        if(valid == 0)
        {
            printf("Invalid phone number! Enter exactly 10 digits.\n");
        }

    } while(valid == 0);

    printf("Enter your email: ");
    scanf("%49s", contacts[count].email);

    count++;

    printf("\nContact Added Successfully!\n");
}

// Function to display all contacts
void displayContact()
{
    int i;

    if(count == 0)
    {
        printf("\nNo contacts available!\n");
    }
    else
    {
        for(i = 0; i < count; i++)
        {
            printf("\n--- Contact %d ---\n", i + 1);
            printf("Name: %s\n", contacts[i].name);
            printf("Phone: %s\n", contacts[i].phone);
            printf("Email: %s\n", contacts[i].email);
        }
    }
}

// Function to search contact
void searchContact()
{
    char name[50];
    char no[15];
    int i;
    int found = 0;

    printf("\nEnter your name: ");
    scanf(" %49[^\n]", name);

    printf("Enter your phone number: ");
    scanf("%14s", no);

    for(i = 0; i < count; i++)
    {
        if(strcmp(contacts[i].name, name) == 0 &&
           strcmp(contacts[i].phone, no) == 0)
        {
            printf("\nContact Found!\n");
            printf("Name: %s\n", contacts[i].name);
            printf("Phone: %s\n", contacts[i].phone);
            printf("Email: %s\n", contacts[i].email);

            found = 1;
            break;
        }
    }

    if(found == 0)
    {
        printf("\nContact Not Found!\n");
    }
}

// Main function
int main()
{
    int choice;

    do
    {
        printf("\n===== CONTACT MANAGEMENT SYSTEM =====\n");
        printf("1. Add Contact\n");
        printf("2. Display Contacts\n");
        printf("3. Search Contact\n");
        printf("4. Exit\n");

        printf("\nEnter your choice: ");
        scanf("%d", &choice);

        switch(choice)
        {
            case 1:
                addContact();
                break;

            case 2:
                displayContact();
                break;

            case 3:
                searchContact();
                break;

            case 4:
                printf("\nExiting Program...\n");
                break;

            default:
                printf("\nInvalid Choice!\n");
        }

    } while(choice != 4);

    return 0;
}