#  Assignment: 10 Unit_2 Linked List Front-Back Split

<p>This document presents the implementation of the specialized <code>FrontBackSplit_npk</code> function within a simplified Singly Linked List (SLL) framework, adhering to a strict C-style logic and naming convention.</p>

---

## Concept: Singly Linked List (SLL) Structure

The underlying data structure is a **Singly Linked List (SLL)**, where each node (`SLL_npk`) is composed of simple integer data (`data_npk`) and a pointer (`next_npk`) to the subsequent node.

| **Component** | **Description** |
| :--- | :--- |
| `SLL_npk` | The node structure, analogous to the `GNode_npk` concept's base structure, but simplified to exclude GLL-specific fields (`flag_npk`, `sublist_npk`). |
| `data_npk` | Simple integer payload of the node. |
| `next_npk` | Pointer to the next node in the sequence. |

<p>The entire implementation maintains the required suffix **<code>_npk</code>** for all functions and variables.</p>

---

## 📐 Algorithm: FrontBackSplit\_npk

The algorithm is designed to fulfill the following problem specification for list splitting:

> Given a list, split it into two sublists — one for the front half, and one for the back half. If the number of elements is **odd**, the **extra element should go in the front list**.
>
> **Example:** $L=\{2, 3, 5, 7, 11\} \rightarrow \text{Front}: \{2, 3, 5\}$, $\text{Back}: \{7, 11\}$.

### **Key Technique: Slow and Fast Pointers**

The `FrontBackSplit_npk` function achieves an $O(N)$ split complexity using two pointers:

1.  **Initialization:**
    * `slow_npk` starts at the list head (`source_npk`).
    * `fast_npk` starts at the second node (`source_npk->next_npk`).
2.  **Traversal Logic:**
    * `fast_npk` moves **two** steps per iteration.
    * `slow_npk` moves **one** step per iteration.
3.  **Split Point Resolution:**
    * By starting `fast_npk` one node ahead, `slow_npk` is guaranteed to stop at the **end of the front half**.
        * **Even Length (N=4):** `slow_npk` stops at node 2. Front: 2, Back: 2.
        * **Odd Length (N=5):** `slow_npk` stops at node 3. Front: 3, Back: 2.
4.  **List Severing:**
    * The link between the two halves is broken by setting `slow_npk->next_npk = NULL;`. The back list begins at the original `slow_npk->next_npk`.

---

## 💻 C++ Code Implementation (Simplified SLL)

```cpp

#include <iostream>
#include <cstdlib>
#include <cstdio> // For C-style I/O functions

// Structure Definition
typedef struct node_npk {
    int data_npk; // Simple integer data
    struct node_npk* next_npk;
} SLL_npk;

// Function Prototypes
SLL_npk* getNode_npk(void);
SLL_npk* createList_npk(void);
void printList_npk(SLL_npk* head_npk);
SLL_npk* insertAtBeginning_npk(SLL_npk* head_npk);
SLL_npk* insertAtEnd_npk(SLL_npk* head_npk);
// SLL_npk* insertAfter_npk(SLL_npk* head_npk); // Removed as search is complex without specific key
SLL_npk* deleteAtBeginning_npk(SLL_npk* head_npk);
SLL_npk* deleteAtEnd_npk(SLL_npk* head_npk);
// SLL_npk* deleteByRoll_npk(SLL_npk* head_npk, int roll_npk); // Removed
// SLL_npk* searchList_npk(SLL_npk* head_npk); // Removed
SLL_npk* reverseList_npk(SLL_npk* head_npk);
int countNodes_npk(SLL_npk* head_npk);
SLL_npk* destroyList_npk(SLL_npk* head_npk);
void FrontBackSplit_npk(SLL_npk* source_npk, SLL_npk** frontRef_npk, SLL_npk** backRef_npk);
void testFrontBackSplit_npk(SLL_npk** headRef_npk); // Passes address of head for modification

// Menu function (Simplified)
int menu_npk()
{
    int choice_npk;
    printf("\n===== Simple Singly Linked List Menu =====\n");
    printf("1. Create List\n");
    printf("2. Print List\n");
    printf("3. Insert at Beginning\n");
    printf("4. Insert at End\n");
    printf("5. Delete at Beginning\n");
    printf("6. Delete at End\n");
    printf("7. Count Nodes\n");
    printf("8. Reverse List\n");
    printf("9. Destroy List\n");
    printf("10. Split List (FrontBackSplit)\n"); // Focus function
    printf("11. Exit\n");
    printf("Enter your choice: ");
    scanf("%d", &choice_npk);
    return choice_npk;
}

// Main Function
int main_npk() {
    SLL_npk* head_npk = NULL;
    int choice_npk;

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
                head_npk = insertAtBeginning_npk(head_npk);
                break;
            }
            case 4:
            {
                head_npk = insertAtEnd_npk(head_npk);
                break;
            }
            case 5:
            {
                head_npk = deleteAtBeginning_npk(head_npk);
                break;
            }
            case 6:
            {
                head_npk = deleteAtEnd_npk(head_npk);
                break;
            }
            case 7:
            {
                printf("Total nodes: %d\n", countNodes_npk(head_npk));
                break;
            }
            case 8:
            {
                head_npk = reverseList_npk(head_npk);
                break;
            }
            case 9:
            {
                head_npk = destroyList_npk(head_npk);
                break;
            }
            case 10:
            {
                testFrontBackSplit_npk(&head_npk);
                break;
            }
            case 11:
            {
                printf("Exiting...\n");
                head_npk = destroyList_npk(head_npk);
                exit(0);
            }
            default:
            {
                printf("Invalid choice.\n");
            }
        }
    }

    return 0;
}

// Node Allocator
SLL_npk* getNode_npk() {
    // Use malloc as in the original C code
    SLL_npk* newNode_npk = (SLL_npk*)malloc(sizeof(SLL_npk));
    if (!newNode_npk) {
        printf("Memory allocation failed.\n");
        exit(1);
    }
    newNode_npk->next_npk = NULL;
    return newNode_npk;
}

// Create Initial List
SLL_npk* createList_npk() {
    SLL_npk* head_npk = NULL, * temp_npk = NULL, * newNode_npk = NULL;
    int choice_npk;
    int data_input_npk;

    printf("Creating a new list.\n");
    while (1) {
        printf("Add element? [1-Yes | 0-No]: ");
        scanf("%d", &choice_npk);

        if (choice_npk == 0)
            break;

        newNode_npk = getNode_npk();
        printf("Enter Data: ");
        scanf("%d", &data_input_npk);
        newNode_npk->data_npk = data_input_npk;

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
        printf("List is empty.\n");
        return;
    }
    printf("List Contents: ");
    while (head_npk != NULL) {
        printf("%d -> ", head_npk->data_npk);
        head_npk = head_npk->next_npk;
    }
    printf("NULL\n");
}

// Insert at Beginning
SLL_npk* insertAtBeginning_npk(SLL_npk* head_npk) {
    SLL_npk* newNode_npk = getNode_npk();
    printf("Enter Data: ");
    scanf("%d", &newNode_npk->data_npk);
    newNode_npk->next_npk = head_npk;
    return newNode_npk;
}

// Insert at End
SLL_npk* insertAtEnd_npk(SLL_npk* head_npk) {
    SLL_npk* newNode_npk = getNode_npk();
    printf("Enter Data: ");
    scanf("%d", &newNode_npk->data_npk);

    if (head_npk == NULL)
        return newNode_npk;

    SLL_npk* temp_npk = head_npk;
    while (temp_npk->next_npk != NULL)
        temp_npk = temp_npk->next_npk;
    temp_npk->next_npk = newNode_npk;
    return head_npk;
}

// Delete at Beginning
SLL_npk* deleteAtBeginning_npk(SLL_npk* head_npk) {
    if (head_npk == NULL) {
        printf("List is empty.\n");
        return NULL;
    }
    SLL_npk* temp_npk = head_npk;
    head_npk = head_npk->next_npk;
    free(temp_npk);
    printf("First node deleted.\n");
    return head_npk;
}

// Delete at End
SLL_npk* deleteAtEnd_npk(SLL_npk* head_npk) {
    if (head_npk == NULL) {
        printf("List is empty.\n");
        return NULL;
    }
    if (head_npk->next_npk == NULL) {
        free(head_npk);
        printf("Last node deleted.\n");
        return NULL;
    }
    SLL_npk* temp_npk = head_npk;
    while (temp_npk->next_npk->next_npk != NULL)
        temp_npk = temp_npk->next_npk;
    free(temp_npk->next_npk);
    temp_npk->next_npk = NULL;
    printf("Last node deleted.\n");
    return head_npk;
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
    while (curr_npk) {
        next_npk = curr_npk->next_npk;
        curr_npk->next_npk = prev_npk;
        prev_npk = curr_npk;
        curr_npk = next_npk;
    }
    printf("List reversed.\n");
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
    printf("All nodes deleted (list destroyed).\n");
    return NULL;
}

// --- Problem Statement Implementation ---

/**
 * Function: FrontBackSplit_npk
 * Purpose: Splits the source list into two sublists: front_npk and back_npk.
 * If the list has an odd number of elements, the extra element goes
 * in the front list. (Uses Slow/Fast Pointer Technique)
 */
void FrontBackSplit_npk(SLL_npk* source_npk, SLL_npk** frontRef_npk, SLL_npk** backRef_npk) {
    SLL_npk* fast_npk;
    SLL_npk* slow_npk;

    // Handle length 0 or 1
    if (source_npk == NULL || source_npk->next_npk == NULL) {
        *frontRef_npk = source_npk;
        *backRef_npk = NULL;
        return;
    }

    slow_npk = source_npk;
    fast_npk = source_npk->next_npk; // Start fast one step ahead

    // Advance fast two nodes, and slow one node.
    // slow stops at the end of the first half (correctly handles odd length)
    while (fast_npk != NULL) {
        fast_npk = fast_npk->next_npk;
        if (fast_npk != NULL) {
            slow_npk = slow_npk->next_npk;
            fast_npk = fast_npk->next_npk;
        }
    }

    // 'slow_npk' is the last node of the front list
    *frontRef_npk = source_npk;
    *backRef_npk = slow_npk->next_npk; // Back list starts after slow_npk

    // Terminate the front list by setting slow->next = NULL
    slow_npk->next_npk = NULL;
}

// Test Function for Split
void testFrontBackSplit_npk(SLL_npk** headRef_npk) {
    SLL_npk* head_npk = *headRef_npk;

    if (head_npk == NULL) {
        printf("List is empty. Cannot split.\n");
        return;
    }

    printf("\n--- Performing FrontBackSplit ---\n");
    printf("Original List: ");
    printList_npk(head_npk);
    
    SLL_npk* front_npk = NULL;
    SLL_npk* back_npk = NULL;

    FrontBackSplit_npk(head_npk, &front_npk, &back_npk);

    printf("\nFront List:\n");
    printList_npk(front_npk);

    printf("\nBack List:\n");
    printList_npk(back_npk);

    // After splitting, the original head is now the head of the front list.
    // The back list must be managed separately. We update the main head to NULL
    // to force a deliberate recreation or use of the front/back list next.
    // For this demonstration, we'll keep the front list as the new main head.
    *headRef_npk = front_npk; 
    
    // Note: The memory for the back list must be freed manually or used elsewhere.
    printf("\nReturning Front List as new main list (Back list retained for possible use or must be freed).\n");
    
    // The main list now only contains the 'front' split. The 'back' list is detached.
    // To prevent memory leak in the running program, we should destroy the detached back list here
    printf("Destroying detached Back List to prevent memory leak:\n");
    destroyList_npk(back_npk);
}


// Custom entry point for the C++ code to use the original C main function logic.
int main() {
    return main_npk();
}
  ````

## Output

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_20.cpp -o Assign_20 } ; if ($?) { .\Assign_20 }

===== Simple Singly Linked List Menu =====
1. Create List
2. Print List
3. Insert at Beginning
4. Insert at End
5. Delete at Beginning
6. Delete at End
7. Count Nodes
8. Reverse List
9. Destroy List
10. Split List (FrontBackSplit)
11. Exit
Enter your choice: 1
Creating a new list.
Add element? [1-Yes | 0-No]: 1
Enter Data: 23
Add element? [1-Yes | 0-No]: 1
Enter Data: 45
Add element? [1-Yes | 0-No]: 1
Enter Data: 56
Add element? [1-Yes | 0-No]: 1
Enter Data: 75
Add element? [1-Yes | 0-No]: 1
Enter Data: 90
Add element? [1-Yes | 0-No]: 0

===== Simple Singly Linked List Menu =====
1. Create List
2. Print List
3. Insert at Beginning
4. Insert at End
5. Delete at Beginning
6. Delete at End
7. Count Nodes
8. Reverse List
9. Destroy List
10. Split List (FrontBackSplit)
11. Exit
Enter your choice: 10

--- Performing FrontBackSplit ---
Original List: List Contents: 23 -> 45 -> 56 -> 75 -> 90 -> NULL

Front List:
List Contents: 23 -> 45 -> 56 -> NULL

Back List:
List Contents: 75 -> 90 -> NULL

Returning Front List as new main list (Back list retained for possible use or must be freed).
Destroying detached Back List to prevent memory leak:
All nodes deleted (list destroyed).

===== Simple Singly Linked List Menu =====
1. Create List
2. Print List
3. Insert at Beginning
4. Insert at End
5. Delete at Beginning
6. Delete at End
7. Count Nodes
8. Reverse List
9. Destroy List
10. Split List (FrontBackSplit)
11. Exit
Enter your choice:

````