## ASSIGNMENT NO - 3 Unit_2

\<p align="center"\>Implementation of Bubble Sort Algorithm on a Doubly Linked List (DLL)\</p\>

-----

## Concept: Bubble Sort on Doubly Linked List (DLL)

**Bubble Sort** is a straightforward sorting algorithm that repeatedly steps through the list, compares **adjacent elements**, and swaps them if they are in the wrong order. This process is repeated until the list is sorted.

Using a **Doubly Linked List (DLL)** for Bubble Sort is beneficial because:

1.  **Bi-directional Traversal:** The DLL allows easy traversal in the forward direction for comparisons, and the `prev` pointer is crucial for efficiently updating links during the swap operation.
2.  **Efficient Swapping:** Unlike a Singly Linked List (SLL) where swapping adjacent nodes requires tracking two to three pointers, in a DLL, a node's links to *both* neighbors can be updated quickly.

The implementation focuses on **swapping the data** within adjacent nodes rather than swapping the nodes themselves, simplifying the pointer management.

-----

## Algorithms

### 1\. `sortListByPrn_npk()` (Bubble Sort Logic)

This function implements the Bubble Sort algorithm by comparing the `roll_no` (the sorting key) of adjacent nodes and swapping their data.

Initialize a flag `swapped_npk = 0` to track if any swaps occurred in a pass.

Use a **do-while loop** that runs as long as `swapped_npk` is `1` (meaning swaps were made in the last pass).

Inside the loop:

1.  Initialize `i_npk = head_npk`.
2.  Traverse the list: `while (i_npk->next_npk != NULL)`.
3.  Set `j_npk = i_npk->next_npk`.
4.  **Comparison:** `if (i_npk->roll_no > j_npk->roll_no)`.
      * If the current node's roll number is greater than the next node's, call `swapData_npk(i_npk, j_npk)` to swap their contents.
      * Set `swapped_npk = 1`.
5.  Move to the next pair: `i_npk = i_npk->next_npk`.

Return the `head_npk`.

### 2\. `swapData_npk()` (Helper Function)

Accepts two node pointers, `a_npk` and `b_npk`.

Uses temporary variables to hold the data from `a_npk`.

Copies the data from `b_npk` to `a_npk`.

Copies the stored temporary data (original data of `a_npk`) to `b_npk`.

-----

## C++ Code Implementation

This code reuses the DLL structure and auxiliary functions from the provided reference DLL code, focusing on the new `sortListByPrn_npk` and its helper `swapData_npk`.

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
void swapData_npk(DLL_npk* a_npk, DLL_npk* b_npk);
DLL_npk* sortListByPrn_npk(DLL_npk* head_npk); 
DLL_npk* destroyList_npk(DLL_npk* head_npk);

// --------------------- Menu Function ---------------------
int menu_npk() {
    int choice_npk;
    cout << "\n========== Doubly Linked List Menu (Bubble Sort) ==========\n";
    cout << "1. Create List\n";
    cout << "2. Print List\n";
    cout << "3. Sort List by Roll No (Bubble Sort)\n";
    cout << "4. Destroy List\n";
    cout << "5. Exit\n";
    cout << "Enter your choice: ";
    cin >> choice_npk;
    return choice_npk;
}

// --------------------- Main Function ---------------------
int main() {
    DLL_npk* head_npk = NULL;
    int choice_npk;

    while (1) {
        choice_npk = menu_npk();
        switch (choice_npk) {
        case 1: 
            head_npk = createList_npk(); 
            break;
        case 2: 
            printList_npk(head_npk); 
            break;
        case 3: 
            head_npk = sortListByPrn_npk(head_npk); 
            break;
        case 4:
            head_npk = destroyList_npk(head_npk);
            break;
        case 5:
            cout << "Exiting program...\n";
            head_npk = destroyList_npk(head_npk); 
            exit(0);
        default:
            cout << "Invalid choice.\n";
        }
    }
    return 0;
}

// Helper function to get a new node
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

// Function to create list
DLL_npk* createList_npk() 
{
    DLL_npk* head_npk = NULL, * temp_npk = NULL, * newNode_npk = NULL;
    int choice_npk;
    while (1) {
        cout << "Add student? [1-Yes | 0-No]: ";
        cin >> choice_npk;
        if (choice_npk == 0) break;
        newNode_npk = getNode_npk();
        newNode_npk->roll_no_npk = rollCounter_npk++;
        cout << "Enter Name: ";
        cin >> newNode_npk->name_npk;
        cout << "Enter Marks: ";
        cin >> newNode_npk->marks_npk;
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

// Function to print list
void printList_npk(DLL_npk* head_npk) 
{
    if (head_npk == NULL) 
    {
        cout << "List is empty.\n";
        return;
    }
    cout << "\n--- Current List ---\n";
    while (head_npk != NULL) 
    {
        cout << "Roll: " << head_npk->roll_no_npk << " | Name: " << head_npk->name_npk << " | Marks: " << head_npk->marks_npk << "\n";
        head_npk = head_npk->next_npk;
    }
}

// Function to swap data between two nodes (used for Bubble Sort)
void swapData_npk(DLL_npk* a_npk, DLL_npk* b_npk) {
    int tempRoll_npk = a_npk->roll_no_npk;
    char tempName_npk[50];
    float tempMarks_npk = a_npk->marks_npk;

    // Swap Roll No
    a_npk->roll_no_npk = b_npk->roll_no_npk;
    b_npk->roll_no_npk = tempRoll_npk;

    // Swap Name
    strcpy(tempName_npk, a_npk->name_npk);
    strcpy(a_npk->name_npk, b_npk->name_npk);
    strcpy(b_npk->name_npk, tempName_npk);

    // Swap Marks
    a_npk->marks_npk = b_npk->marks_npk;
    b_npk->marks_npk = tempMarks_npk;
}

/* Function: sortListByPrn_npk() 
Purpose: Sorts the DLL by roll_no using Bubble Sort (swapping data)
*/
DLL_npk* sortListByPrn_npk(DLL_npk* head_npk) {
    if (head_npk == NULL || head_npk->next_npk == NULL) {
        cout << "List is empty or has only one node. No sorting needed.\n";
        return head_npk;
    }

    DLL_npk* i_npk, * j_npk;
    int swapped_npk;

    do {
        swapped_npk = 0;
        i_npk = head_npk;

        // Traverse up to the second-to-last element
        while (i_npk->next_npk != NULL) {
            j_npk = i_npk->next_npk;
            
            // Compare and swap data based on roll_no
            if (i_npk->roll_no_npk > j_npk->roll_no_npk) {
                swapData_npk(i_npk, j_npk);
                swapped_npk = 1; // Mark that a swap occurred
            }
            i_npk = i_npk->next_npk;
        }
    } while (swapped_npk);

    cout << "List sorted by Roll No (Bubble Sort).\n";
    return head_npk;
}

// Function to destroy list
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
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_13.cpp -o Assign_13 } ; if ($?) { .\Assign_13 }

========== Doubly Linked List Menu (Bubble Sort) ==========
1. Create List
2. Print List
3. Sort List by Roll No (Bubble Sort)
4. Destroy List
5. Exit
Enter your choice: 1
Add student? [1-Yes | 0-No]: 1
Enter Name: Nandini
Enter Marks: 99
Add student? [1-Yes | 0-No]: 0

========== Doubly Linked List Menu (Bubble Sort) ==========
1. Create List
2. Print List
3. Sort List by Roll No (Bubble Sort)
4. Destroy List
5. Exit
Enter your choice: 2

--- Current List ---
Roll: 1 | Name: Nandini | Marks: 99

========== Doubly Linked List Menu (Bubble Sort) ==========
1. Create List
2. Print List
3. Sort List by Roll No (Bubble Sort)
4. Destroy List
5. Exit
Enter your choice:

```