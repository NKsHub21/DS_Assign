

# ASSIGNMENT NO - 1 Unit_2
<p align="center">Implementation of Singly Linked List to Manage ‘Vertex Club’ Membership Records</p>

---

## Concept: The Singly Linked List

A **Singly Linked List** is a fundamental linear data structure where elements (nodes) are sequentially linked together using **pointers**. Each node holds two key pieces of information:

1.  **Data Field:** Contains the actual member information (PRN, name, and year).
2.  **Pointer Field** (`next_npk`): Stores the memory address of the next node in the sequence.

In the 'Vertex Club' structure:
* The first node is the **President** (referenced by the `head` pointer).
* The last node is the **Secretary** (its `next_npk` pointer is `NULL`).

---

## Algorithms

### 1. Insert at Beginning (New President)

Create newNode_npk and accept data.

Set newNode_npk->next_npk = head_npk.

Update head_npk = newNode_npk.

Return head_npk.


### 2. Delete by PRN

Traverse list using temp_npk and prev_npk pointers.

If head_npk matches PRN, update head_npk and free.

If temp_npk matches PRN, set prev_npk->next_npk = temp_npk->next_npk.

Free temp_npk and return head_npk.


### 3. Reverse List

Initialize prev_npk = NULL, curr_npk = head_npk, next_npk = NULL.

Loop while curr_npk is not NULL:
a. next_npk = curr_npk->next_npk (Save next).
b. curr_npk->next_npk = prev_npk (Reverse link).
c. prev_npk = curr_npk (Move prev forward).
d. curr_npk = next_npk (Move curr forward).

Return prev_npk as the new head.


### 4. Concatenation

Traverse list 1 (head1_npk) until the last node (temp_npk->next_npk == NULL).

Set temp_npk->next_npk = head2_npk (Link the end of list 1 to the start of list 2).

Return head1_npk.


---

## C++ Code Implementation

```cpp
#include <iostream>
#include <cstdlib> 
#include <cstring> 

using namespace std;

// Structure Definition
typedef struct vertexClub_npk {
    int prn_npk; 
    char name_npk[50];
    char year_npk[10]; 
    struct vertexClub_npk* next_npk;
} SLL_npk;

// Function Prototypes
SLL_npk* getNode_npk(void);
SLL_npk* createList_npk(void);
void printList_npk(SLL_npk* head_npk);
SLL_npk* insertAtBeginning_npk(SLL_npk* head_npk);
SLL_npk* insertAtEnd_npk(SLL_npk* head_npk);
SLL_npk* deleteAtBeginning_npk(SLL_npk* head_npk);
SLL_npk* deleteAtEnd_npk(SLL_npk* head_npk);
SLL_npk* deleteByPrn_npk(SLL_npk* head_npk, int prn_npk);
SLL_npk* searchList_npk(SLL_npk* head_npk);
SLL_npk* reverseList_npk(SLL_npk* head_npk);
int countNodes_npk(SLL_npk* head_npk);
SLL_npk* destroyList_npk(SLL_npk* head_npk);
SLL_npk* sortListByPrn_npk(SLL_npk* head_npk);
SLL_npk* concatLists_npk(SLL_npk* head1_npk, SLL_npk* head2_npk);

// Global PRN Counter
static int prnCounter_npk = 1001;

// Helper to accept common member data
void getMemberData_npk(SLL_npk* node_npk) {
    node_npk->prn_npk = prnCounter_npk++;
    cout << "Enter Name: ";
    cin >> node_npk->name_npk;
    cout << "Enter Year (e.g., Second, Third, Final): ";
    cin >> node_npk->year_npk;
}

int menu_npk()
{
    int choice_npk;
    cout << "\n===== Vertex Club Membership Menu =====\n";
    cout << "1. Create List\n";
    cout << "2. Print List\n";
    cout << "3. Search by PRN/Name/Year\n";
    cout << "4. Insert at Beginning (New President)\n";
    cout << "5. Insert at End (New Secretary)\n";
    cout << "6. Delete at Beginning (Remove President)\n";
    cout << "7. Delete at End (Remove Secretary)\n";
    cout << "8. Delete by PRN\n";
    cout << "9. Count Members\n";
    cout << "10. Reverse List\n";
    cout << "11. Sort List by PRN\n";
    cout << "12. Concatenate with a Second List\n";
    cout << "13. Destroy List\n";
    cout << "14. Exit\n";
    cout << "Enter your choice: ";
    cin >> choice_npk;
    return choice_npk;
}

// Main Function
int main() {
    SLL_npk* head_npk = NULL;
    SLL_npk* head2_npk = NULL;
    int choice_npk, prn_npk;

    while (1) {
        choice_npk = menu_npk();

        switch (choice_npk) 
        {
            case 1:
            {
                head_npk = createList_npk();
                break;
            }
            case 2:
            {
                printList_npk(head_npk);
                break;
            }
            case 3:
            {
                searchList_npk(head_npk);
                break;
            }
            case 4:
            {
                head_npk = insertAtBeginning_npk(head_npk);
                break;
            }
            case 5:
            {
                head_npk = insertAtEnd_npk(head_npk);
                break;
            }
            case 6:
            {
                head_npk = deleteAtBeginning_npk(head_npk);
                break;
            }
            case 7:
            {
                head_npk = deleteAtEnd_npk(head_npk);
                break;
            }
            case 8:
            {
                cout << "Enter PRN to delete: ";
                cin >> prn_npk;
                head_npk = deleteByPrn_npk(head_npk, prn_npk);
                break;
            }
            case 9:
            {
                cout << "Total members: " << countNodes_npk(head_npk) << "\n";
                break;
            }
            case 10:
            {
                head_npk = reverseList_npk(head_npk);
                break;
            }
            case 11:
            {
                head_npk = sortListByPrn_npk(head_npk);
                break;
            }
            case 12:
            {
                cout << "\n--- Creating Second List for Concatenation ---\n";
                head2_npk = createList_npk();
                head_npk = concatLists_npk(head_npk, head2_npk);
                head2_npk = NULL; 
                break;
            }
            case 13:
            {
                head_npk = destroyList_npk(head_npk);
                break;
            }
            case 14:
            {
                cout << "Exiting...\n";
                head_npk = destroyList_npk(head_npk);
                exit(0);
            }
            default:
            {
                cout << "Invalid choice.\n";
            }
        }
    }

    return 0;
}

// Node Allocator
SLL_npk* getNode_npk() {
    SLL_npk* newNode_npk = (SLL_npk*)malloc(sizeof(SLL_npk));
    if (!newNode_npk) {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    newNode_npk->next_npk = NULL;
    return newNode_npk;
}

// Create Initial List
SLL_npk* createList_npk() {
    SLL_npk* head_npk = NULL, * temp_npk = NULL, * newNode_npk = NULL;
    int choice_npk;

    while (1) {
        cout << "Add student member? [1-Yes | 0-No]: ";
        cin >> choice_npk;
        
        if (choice_npk == 0)
            break;

        newNode_npk = getNode_npk();
        getMemberData_npk(newNode_npk);

        if (head_npk == NULL) 
        {
            head_npk = newNode_npk;
        }
        else 
        {
            temp_npk = head_npk;
            while (temp_npk->next_npk != NULL)
                temp_npk = temp_npk->next_npk;

            temp_npk->next_npk = newNode_npk;
        }
    }
    return head_npk;
}

// Print List
void printList_npk(SLL_npk* head_npk) {
    if (head_npk == NULL) {
        cout << "List is empty.\n";
        return;
    }
    int count_npk = 1;
    SLL_npk* current_npk = head_npk;
    SLL_npk* last_npk = NULL;
    
    // Find the last node for Secretary identification
    if (current_npk != NULL) {
        last_npk = current_npk;
        while (last_npk->next_npk != NULL) {
            last_npk = last_npk->next_npk;
        }
    }

    while (current_npk != NULL) {
        const char* role_npk = "Member";
        if (count_npk == 1) {
            role_npk = "President";
        } else if (current_npk == last_npk) {
            role_npk = "Secretary";
        }

        cout << "Member " << count_npk << " (" << role_npk << "): PRN: " 
             << current_npk->prn_npk << " | Name: " << current_npk->name_npk 
             << " | Year: " << current_npk->year_npk << "\n";
        
        current_npk = current_npk->next_npk;
        count_npk++;
    }
}

// Insert at Beginning
SLL_npk* insertAtBeginning_npk(SLL_npk* head_npk) {
    SLL_npk* newNode_npk = getNode_npk();
    getMemberData_npk(newNode_npk);
    newNode_npk->next_npk = head_npk;
    cout << "New President added.\n";
    return newNode_npk;
}

// Insert at End
SLL_npk* insertAtEnd_npk(SLL_npk* head_npk) {
    SLL_npk* newNode_npk = getNode_npk();
    getMemberData_npk(newNode_npk);

    if (head_npk == NULL) {
        cout << "New Secretary/President added to empty list.\n";
        return newNode_npk;
    }

    SLL_npk* temp_npk = head_npk;
    while (temp_npk->next_npk != NULL)
        temp_npk = temp_npk->next_npk;
    temp_npk->next_npk = newNode_npk;
    cout << "New Secretary added.\n";
    return head_npk;
}

// Delete at Beginning
SLL_npk* deleteAtBeginning_npk(SLL_npk* head_npk) {
    if (head_npk == NULL) {
        cout << "List is empty.\n";
        return NULL;
    }
    SLL_npk* temp_npk = head_npk;
    head_npk = head_npk->next_npk;
    free(temp_npk);
    cout << "President node deleted.\n";
    return head_npk;
}

// Delete at End
SLL_npk* deleteAtEnd_npk(SLL_npk* head_npk) {
    if (head_npk == NULL) {
        cout << "List is empty.\n";
        return NULL;
    }
    if (head_npk->next_npk == NULL) {
        free(head_npk);
        cout << "Secretary/Only node deleted.\n";
        return NULL;
    }
    SLL_npk* temp_npk = head_npk;
    while (temp_npk->next_npk->next_npk != NULL)
        temp_npk = temp_npk->next_npk;
    free(temp_npk->next_npk);
    temp_npk->next_npk = NULL;
    cout << "Secretary node deleted.\n";
    return head_npk;
}

// Delete by PRN
SLL_npk* deleteByPrn_npk(SLL_npk* head_npk, int prn_npk) {
    if (head_npk == NULL) {
        cout << "List is empty.\n";
        return NULL;
    }
    if (head_npk->prn_npk == prn_npk) {
        SLL_npk* temp_npk = head_npk;
        head_npk = head_npk->next_npk;
        free(temp_npk);
        cout << "Deleted PRN " << prn_npk << ".\n";
        return head_npk;
    }
    SLL_npk* temp_npk = head_npk, * prev_npk = NULL;
    while (temp_npk != NULL && temp_npk->prn_npk != prn_npk) {
        prev_npk = temp_npk;
        temp_npk = temp_npk->next_npk;
    }
    if (temp_npk == NULL) {
        cout << "PRN " << prn_npk << " not found.\n";
        return head_npk;
    }
    prev_npk->next_npk = temp_npk->next_npk;
    free(temp_npk);
    cout << "Deleted PRN " << prn_npk << ".\n";
    return head_npk;
}

// Search by PRN / Name / Year
SLL_npk* searchList_npk(SLL_npk* head_npk) {
    int choice_npk, rno_npk;
    char name_npk[50], year_npk[10];

    if (head_npk == NULL) {
        cout << "List is empty. Cannot search.\n";
        return NULL;
    }

    cout << "\nSearch by: 1.PRN 2.Name 3.Year\nEnter choice: ";
    cin >> choice_npk;

    SLL_npk* current_npk = head_npk;
    bool found_npk = false;

    switch (choice_npk) {
    case 1:
        cout << "Enter PRN: ";
        cin >> rno_npk;
        while (current_npk) {
            if (current_npk->prn_npk == rno_npk) {
                cout << "Found: Name: " << current_npk->name_npk << " | Year: " << current_npk->year_npk << "\n";
                return current_npk;
            }
            current_npk = current_npk->next_npk;
        }
        break;
    case 2:
        cout << "Enter Name: ";
        cin >> name_npk;
        while (current_npk) {
            if (strcmp(current_npk->name_npk, name_npk) == 0) {
                cout << "Found: PRN: " << current_npk->prn_npk << " | Year: " << current_npk->year_npk << "\n";
                return current_npk;
            }
            current_npk = current_npk->next_npk;
        }
        break;
    case 3:
        cout << "Enter Year: ";
        cin >> year_npk;
        while (current_npk) {
            if (strcmp(current_npk->year_npk, year_npk) == 0) {
                cout << "Found: PRN: " << current_npk->prn_npk << " | Name: " << current_npk->name_npk << "\n";
                found_npk = true;
            }
            current_npk = current_npk->next_npk;
        }
        if (found_npk) return head_npk; 
        break;
    default:
        cout << "Invalid choice.\n";
        return NULL;
    }
    cout << "Record not found.\n";
    return NULL;
}

// Count total nodes
int countNodes_npk(SLL_npk* head_npk) {
    int count_npk = 0;
    while (head_npk) {
        count_npk++;
        head_npk = head_npk->next_npk;
    }
    return count_npk;
}

// Reverse Linked List
SLL_npk* reverseList_npk(SLL_npk* head_npk) {
    SLL_npk* prev_npk = NULL, * curr_npk = head_npk, * next_npk = NULL;
    if (head_npk == NULL) {
        cout << "List is empty. Cannot reverse.\n";
        return NULL;
    }
    SLL_npk* old_head_npk = head_npk;
    while (curr_npk) {
        next_npk = curr_npk->next_npk;
        curr_npp->next_npk = prev_npk;
        prev_npk = curr_npk;
        curr_npk = next_npk;
    }
    cout << "List reversed. New President: " << prev_npk->name_npk << ", New Secretary: " 
         << old_head_npk->name_npk << ".\n";
    return prev_npk;
}

// Destroy Entire List
SLL_npk* destroyList_npk(SLL_npk* head_npk) {
    SLL_npk* temp_npk;
    while (head_npk) {
        temp_npk = head_npk;
        head_npk = head_npk->next_npk;
        free(temp_npk);
    }
    cout << "All nodes deleted.\n";
    return NULL;
}

// Function to swap data between two nodes (used for sorting)
void swapData_npk(SLL_npk* a_npk, SLL_npk* b_npk) {
    int tempPrn_npk = a_npk->prn_npk;
    char tempName_npk[50];
    char tempYear_npk[10];

    // Swap PRN
    a_npk->prn_npk = b_npk->prn_npk;
    b_npk->prn_npk = tempPrn_npk;

    // Swap Name
    strcpy(tempName_npk, a_npk->name_npk);
    strcpy(a_npk->name_npk, b_npk->name_npk);
    strcpy(b_npk->name_npk, tempName_npk);

    // Swap Year
    strcpy(tempYear_npk, a_npk->year_npk);
    strcpy(a_npk->year_npk, b_npk->year_npk);
    strcpy(b_npk->year_npk, tempYear_npk);
}

// Sorts the linked list by PRN
SLL_npk* sortListByPrn_npk(SLL_npk* head_npk) {
    if (head_npk == NULL || head_npk->next_npk == NULL) {
        cout << "List is empty or has only one node. No sorting needed.\n";
        return head_npk;
    }

    SLL_npk* i_npk, * j_npk;
    int swapped_npk;

    do {
        swapped_npk = 0;
        i_npk = head_npk;

        while (i_npk->next_npk != NULL) {
            j_npk = i_npk->next_npk;
            // Compare and swap data based on PRN
            if (i_npk->prn_npk > j_npk->prn_npk) {
                swapData_npk(i_npk, j_npk);
                swapped_npk = 1;
            }
            i_npk = i_npk->next_npk;
        }
    } while (swapped_npk);

    cout << "List sorted by PRN.\n";
    return head_npk;
}

// Concatenates the second list to the end of the first list
SLL_npk* concatLists_npk(SLL_npk* head1_npk, SLL_npk* head2_npk) {
    if (head1_npk == NULL) {
        cout << "First list was empty. Returning second list.\n";
        return head2_npk;
    }
    if (head2_npk == NULL) {
        cout << "Second list was empty. Returning first list.\n";
        return head1_npk;
    }

    SLL_npk* temp_npk = head1_npk;
    while (temp_npk->next_npk != NULL) {
        temp_npk = temp_npk->next_npk;
    }
    temp_npk->next_npk = head2_npk;
    cout << "Lists concatenated. Second list members added to the end of the first list.\n";
    return head1_npk;
}


##Output

PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_11.cpp -o Assign_11 } ; if ($?) { .\Assign_11 }

===== Vertex Club Membership Menu =====
1. Create List
2. Print List
3. Search by PRN/Name/Year
4. Insert at Beginning (New President)
5. Insert at End (New Secretary)
6. Delete at Beginning (Remove President)
7. Delete at End (Remove Secretary)
8. Delete by PRN
9. Count Members
10. Reverse List
11. Sort List by PRN
12. Concatenate with a Second List
13. Destroy List
14. Exit
Enter your choice: 1
Add student member? [1-Yes | 0-No]: 1
Enter Name: Nandini
Enter Year (e.g., Second, Third, Final): Second
Add student member? [1-Yes | 0-No]: 0

===== Vertex Club Membership Menu =====
1. Create List
2. Print List
3. Search by PRN/Name/Year
4. Insert at Beginning (New President)
5. Insert at End (New Secretary)
6. Delete at Beginning (Remove President)
7. Delete at End (Remove Secretary)
8. Delete by PRN
9. Count Members
10. Reverse List
11. Sort List by PRN
12. Concatenate with a Second List
13. Destroy List
14. Exit
Enter your choice: 2
Member 1 (President): PRN: 1001 | Name: Nandini | Year: Second

===== Vertex Club Membership Menu =====
1. Create List
2. Print List
3. Search by PRN/Name/Year
4. Insert at Beginning (New President)
5. Insert at End (New Secretary)
6. Delete at Beginning (Remove President)
7. Delete at End (Remove Secretary)
8. Delete by PRN
9. Count Members
10. Reverse List
11. Sort List by PRN
12. Concatenate with a Second List
13. Destroy List
14. Exit
Enter your choice:


