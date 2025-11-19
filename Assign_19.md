## ASSIGNMENT NO - 9 Unit_2

\<p align="center"\>Implementation of Doubly Linked List (DLL) with Comprehensive Insertion and Deletion Operations\</p\>

-----

## Concept: Doubly Linked List (DLL)

A **Doubly Linked List (DLL)** is a linear data structure where each element, called a node, is connected to the next node and the previous node. This structure allows **bi-directional traversal** (both forward and backward).

Each node contains three parts:

1.  **Data Field:** Stores the actual information (e.g., student data, in this case, Roll No, Name, Marks).
2.  **`next_npk` Pointer:** Points to the succeeding node.
3.  **`prev_npk` Pointer:** Points to the preceding node.

The list is managed by a `head_npk` pointer, which points to the first node.

-----

## Algorithms for Insertion and Deletion (All Cases)

### A) Insertion Cases

| Operation | Scenario | Algorithm Summary |
| :--- | :--- | :--- |
| **1. Insert at Beginning** (`insertAtBeginning_npk`) | Inserts a new node as the **President** of the list. | Update `newNode_npk->next_npk = head_npk`. Update `head_npk->prev_npk = newNode_npk` (if `head_npk` is not `NULL`). Set `head_npk = newNode_npk`. |
| **2. Insert at End** (`insertAtEnd_npk`) | Inserts a new node as the **Secretary** of the list. | Traverse to the last node (`temp_npk`). Set `temp_npk->next_npk = newNode_npk`. Set `newNode_npk->prev_npk = temp_npk`. |
| **3. Insert at Specific Position** (`insertAfterRoll_npk`) | Inserts a node **after** a target node (identified by Roll No). | Find the target node (`temp_npk`). Set `newNode_npk->next_npk = temp_npk->next_npk`. Set `newNode_npk->prev_npk = temp_npk`. Update links of the node after `temp_npk`: `temp_npk->next_npk->prev_npk = newNode_npk` (if not last node). Set `temp_npk->next_npk = newNode_npk`. |

-----

### B) Deletion Cases

| Operation | Scenario | Algorithm Summary |
| :--- | :--- | :--- |
| **1. Delete at Beginning** (`deleteAtBeginning_npk`) | Deletes the first node (**President**). | Store `head_npk` in `temp_npk`. Set `head_npk = head_npk->next_npk`. Update new `head_npk->prev_npk = NULL` (if not empty). Free `temp_npk`. |
| **2. Delete at End** (`deleteAtEnd_npk`) | Deletes the last node (**Secretary**). | Traverse to the last node (`temp_npk`). Update the second-to-last node's link: `temp_npk->prev_npk->next_npk = NULL`. Free `temp_npk`. |
| **3. Delete by Specific Data** (`deleteByRoll_npk`) | Deletes a node identified by its **Roll No**. | Find the target node (`temp_npk`). Update the previous node's link: `temp_npk->prev_npk->next_npk = temp_npk->next_npk`. Update the next node's link: `temp_npk->next_npk->prev_npk = temp_npk->prev_npk`. Handle special cases (head/tail deletion) using conditional checks. Free `temp_npk`. |

-----

## C++ Code Implementation

```cpp
#include <iostream>
#include <cstdlib>
#include <cstring> 

using namespace std;

// --------------------- Node Structure ---------------------
typedef struct student_npk {
    int roll_no_npk;
    char name_npk[50];
    float marks_npk;
    struct student_npk* prev_npk;
    struct student_npk* next_npk;
} DLL_npk;

// --------------------- Global Counter ---------------------
static int rollCounter_npk = 1;

// --------------------- Function Prototypes ---------------------
DLL_npk* getNode_npk();
DLL_npk* createList_npk();
void printList_npk(DLL_npk* head_npk);

// A) Insertion Cases
DLL_npk* insertAtBeginning_npk(DLL_npk* head_npk);
DLL_npk* insertAtEnd_npk(DLL_npk* head_npk);
DLL_npk* insertAfterRoll_npk(DLL_npk* head_npk, int targetRoll_npk);

// B) Deletion Cases
DLL_npk* deleteAtBeginning_npk(DLL_npk* head_npk);
DLL_npk* deleteAtEnd_npk(DLL_npk* head_npk);
DLL_npk* deleteByRoll_npk(DLL_npk* head_npk, int roll_npk);

// Utility
DLL_npk* destroyList_npk(DLL_npk* head_npk);

// Helper function to get student data
void getStudentData_npk(DLL_npk* newNode_npk) {
    newNode_npk->roll_no_npk = rollCounter_npk++;
    cout << "Enter Name: ";
    cin >> newNode_npk->name_npk;
    cout << "Enter Marks: ";
    cin >> newNode_npk->marks_npk;
}

// --------------------- Menu Function ---------------------
int menu_npk() {
    int choice_npk;
    cout << "\n========== Doubly Linked List Operations Menu ==========\n";
    cout << "1. Create List\n";
    cout << "2. Print List\n";
    cout << "3. Insert at Beginning\n";
    cout << "4. Insert at End\n";
    cout << "5. Insert After Specific Roll No\n";
    cout << "6. Delete at Beginning\n";
    cout << "7. Delete at End\n";
    cout << "8. Delete by Specific Roll No\n";
    cout << "9. Destroy List\n";
    cout << "10. Exit\n";
    cout << "Enter your choice: ";
    cin >> choice_npk;
    return choice_npk;
}

// --------------------- Main Function ---------------------
int main() {
    DLL_npk* head_npk = NULL;
    int choice_npk, roll_npk;

    while (1) {
        choice_npk = menu_npk();
        switch (choice_npk) {
        case 1: head_npk = createList_npk(); break;
        case 2: printList_npk(head_npk); break;
        case 3: head_npk = insertAtBeginning_npk(head_npk); break;
        case 4: head_npk = insertAtEnd_npk(head_npk); break;
        case 5:
            cout << "Enter roll no after which to insert: ";
            cin >> roll_npk;
            head_npk = insertAfterRoll_npk(head_npk, roll_npk);
            break;
        case 6: head_npk = deleteAtBeginning_npk(head_npk); break;
        case 7: head_npk = deleteAtEnd_npk(head_npk); break;
        case 8:
            cout << "Enter roll no to delete: ";
            cin >> roll_npk;
            head_npk = deleteByRoll_npk(head_npk, roll_npk);
            break;
        case 9:
            head_npk = destroyList_npk(head_npk);
            break;
        case 10:
            cout << "Exiting program...\n";
            head_npk = destroyList_npk(head_npk);
            exit(0);
        default:
            cout << "Invalid choice.\n";
        }
    }
    return 0;
}

// Node Allocator
DLL_npk* getNode_npk() 
{
    DLL_npk* newNode_npk = (DLL_npk*)malloc(sizeof(DLL_npk));
    if (!newNode_npk) 
    {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    newNode_npk->prev_npk = NULL;
    newNode_npk->next_npk = NULL;
    return newNode_npk;
}

// Create Initial List
DLL_npk* createList_npk() 
{
    DLL_npk* head_npk = NULL, * temp_npk = NULL, * newNode_npk = NULL;
    int choice_npk;
    while (1) {
        cout << "Add student? [1-Yes | 0-No]: ";
        cin >> choice_npk;
        if (choice_npk == 0) break;
        newNode_npk = getNode_npk();
        getStudentData_npk(newNode_npk);
        if (!head_npk) head_npk = newNode_npk;
        else {
            temp_npk = head_npk;
            while (temp_npk->next_npk) temp_npk = temp_npk->next_npk;
            temp_npk->next_npk = newNode_npk;
            newNode_npk->prev_npk = temp_npk;
        }
    }
    return head_npk;
}

// Print List
void printList_npk(DLL_npk* head_npk) 
{
    if (head_npk == NULL) 
    {
        cout << "List is empty.\n";
        return;
    }
    cout << "\n--- Current DLL (Head -> Tail) ---\n";
    while (head_npk != NULL) 
    {
        cout << "Roll: " << head_npk->roll_no_npk << " | Name: " << head_npk->name_npk << " | Marks: " << head_npk->marks_npk << "\n";
        head_npk = head_npk->next_npk;
    }
}

// --------------------- A) Insertion Cases ---------------------

DLL_npk* insertAtBeginning_npk(DLL_npk* head_npk) {
    DLL_npk* newNode_npk = getNode_npk();
    getStudentData_npk(newNode_npk);
    
    // 1. New node points to old head
    newNode_npk->next_npk = head_npk; 
    
    // 2. Old head's prev points to new node (if list not empty)
    if (head_npk) head_npk->prev_npk = newNode_npk; 
    
    // 3. Update head
    cout << "Node inserted at beginning.\n";
    return newNode_npk;
}

DLL_npk* insertAtEnd_npk(DLL_npk* head_npk) {
    DLL_npk* newNode_npk = getNode_npk();
    getStudentData_npk(newNode_npk);
    
    if (!head_npk) return newNode_npk;

    DLL_npk* temp_npk = head_npk;
    // 1. Traverse to the last node
    while (temp_npk->next_npk) temp_npk = temp_npk->next_npk;
    
    // 2. Link last node to new node
    temp_npk->next_npk = newNode_npk;
    
    // 3. New node's prev points to old last node
    newNode_npk->prev_npk = temp_npk;
    
    cout << "Node inserted at end.\n";
    return head_npk;
}

DLL_npk* insertAfterRoll_npk(DLL_npk* head_npk, int targetRoll_npk) {
    if (!head_npk) {
        cout << "List is empty. Cannot insert after roll.\n";
        return NULL;
    }

    DLL_npk* temp_npk = head_npk;
    // 1. Find the target node
    while (temp_npk && temp_npk->roll_no_npk != targetRoll_npk) temp_npk = temp_npk->next_npk;
    
    if (!temp_npk) {
        cout << "Roll " << targetRoll_npk << " not found.\n";
        return head_npk;
    }

    DLL_npk* newNode_npk = getNode_npk();
    getStudentData_npk(newNode_npk);
    
    // 2. Link new node to the node after temp
    newNode_npk->next_npk = temp_npk->next_npk;
    newNode_npk->prev_npk = temp_npk;
    
    // 3. If temp is not the last node, update the next node's prev pointer
    if (temp_npk->next_npk) temp_npk->next_npk->prev_npk = newNode_npk;
    
    // 4. Link temp node to new node
    temp_npk->next_npk = newNode_npk;
    
    cout << "Node inserted after Roll " << targetRoll_npk << ".\n";
    return head_npk;
}

// --------------------- B) Deletion Cases ---------------------

DLL_npk* deleteAtBeginning_npk(DLL_npk* head_npk) {
    if (!head_npk) {
        cout << "List is empty. Nothing to delete.\n";
        return NULL;
    }
    
    DLL_npk* temp_npk = head_npk;
    head_npk = head_npk->next_npk;
    
    // 1. Update the new head's prev pointer
    if (head_npk) head_npk->prev_npk = NULL; 
    
    // 2. Free the old head
    free(temp_npk);
    cout << "Node deleted from beginning.\n";
    return head_npk;
}

DLL_npk* deleteAtEnd_npk(DLL_npk* head_npk) {
    if (!head_npk) {
        cout << "List is empty. Nothing to delete.\n";
        return NULL;
    }
    
    DLL_npk* temp_npk = head_npk;
    if (!temp_npk->next_npk) { 
        // Single node case
        free(temp_npk);
        cout << "Only node deleted from end.\n";
        return NULL;
    }
    
    // 1. Traverse to the last node
    while (temp_npk->next_npk) temp_npk = temp_npk->next_npk;
    
    // 2. Update the second-to-last node's next pointer
    temp_npk->prev_npk->next_npk = NULL;
    
    // 3. Free the last node
    free(temp_npk);
    cout << "Node deleted from end.\n";
    return head_npk;
}

DLL_npk* deleteByRoll_npk(DLL_npk* head_npk, int roll_npk) {
    if (!head_npk) {
        cout << "List is empty. Cannot delete.\n";
        return NULL;
    }
    
    DLL_npk* temp_npk = head_npk;
    // 1. Find the target node
    while (temp_npk && temp_npk->roll_no_npk != roll_npk) temp_npk = temp_npk->next_npk;
    
    if (!temp_npk) {
        cout << "Roll " << roll_npk << " not found.\n";
        return head_npk;
    }
    
    // 2. Handle head node deletion
    if (temp_npk->prev_npk == NULL) {
        head_npk = temp_npk->next_npk;
        if (head_npk) head_npk->prev_npk = NULL;
    } 
    // 3. Handle deletion of middle/tail node
    else {
        temp_npk->prev_npk->next_npk = temp_npk->next_npk;
        // 4. Update the next node's prev pointer (if not tail)
        if (temp_npk->next_npk) temp_npk->next_npk->prev_npk = temp_npk->prev_npk;
    }
    
    free(temp_npk);
    cout << "Roll " << roll_npk << " deleted.\n";
    return head_npk;
}

// Utility Function
DLL_npk* destroyList_npk(DLL_npk* head_npk) {
    DLL_npk* temp_npk;
    while (head_npk) {
        temp_npk = head_npk;
        head_npk = head_npk->next_npk;
        free(temp_npk);
    }
    cout << "List destroyed.\n";
    return NULL;
}
```

-----

## Output

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_19.cpp -o Assign_19 } ; if ($?) { .\Assign_19 }

========== Doubly Linked List Operations Menu ==========
1. Create List
2. Print List
3. Insert at Beginning
4. Insert at End
5. Insert After Specific Roll No
6. Delete at Beginning
7. Delete at End
8. Delete by Specific Roll No
9. Destroy List
10. Exit
Enter your choice: 1
Add student? [1-Yes | 0-No]: 1
Enter Name: Nandini
Enter Marks: 99
Add student? [1-Yes | 0-No]: 1 
Enter Name: Krish
Enter Marks: 98
Add student? [1-Yes | 0-No]: 1
Enter Name: Maitri
Enter Marks: 89
Add student? [1-Yes | 0-No]: 0

========== Doubly Linked List Operations Menu ==========
1. Create List
2. Print List
3. Insert at Beginning
4. Insert at End
5. Insert After Specific Roll No
6. Delete at Beginning
7. Delete at End
8. Delete by Specific Roll No
9. Destroy List
10. Exit
Enter your choice: 2

--- Current DLL (Head -> Tail) ---
Roll: 1 | Name: Nandini | Marks: 99
Roll: 2 | Name: Krish | Marks: 98
Roll: 3 | Name: Maitri | Marks: 89

========== Doubly Linked List Operations Menu ==========
1. Create List
2. Print List
3. Insert at Beginning
4. Insert at End
5. Insert After Specific Roll No
6. Delete at Beginning
7. Delete at End
8. Delete by Specific Roll No
9. Destroy List
10. Exit
Enter your choice:
````