```markdown
# ASSIGNMENT NO - 08 Unit_2
<p align="center">Doubly Linked List (DLL) Implementation with Bubble Sort</p>

---

## Doubly Linked List Representation

A **Doubly Linked List (DLL)** is a linear data structure where each node, often representing a student record in this implementation, contains three primary fields:

1.  **Data Fields**: Stores the actual information ($\text{roll\_no}$, $\text{name}$, $\text{marks}$).
2.  **Next Pointer Field** (`next\_npk`): Points to the successor node ($\rightarrow$).
3.  **Previous Pointer Field** (`prev\_npk`): Points to the predecessor node ($\leftarrow$).

This structure permits **bi-directional traversal** (forward and backward).

| DLL Advantages | DLL Limitations |
| :--- | :--- |
| Traversal in both directions is possible. | Requires extra memory for the `prev\_npk` pointer. |
| Deletion/Insertion are more efficient as both neighbors are directly accessible. | Implementation and maintenance are slightly more complex. |

---

## Algorithm: Bubble Sort on DLL (by Marks)

The Bubble Sort algorithm is adapted for the Doubly Linked List to sort the student records based on their $\text{marks}$ in ascending order. Since it's a DLL, we can swap the **data fields** of the nodes instead of re-linking the pointers, simplifying the logic.

### 1. Sorting Logic

```

1.  Start.
2.  If the list is empty or has only one node, return.
3.  Set a flag swapped\_npk = true.
4.  Set last\_npk = NULL (pointer to the last sorted node).
5.  Do-While loop (while swapped\_npk is true):
    a. Set swapped\_npk = false.
    b. Set current\_npk = head\_npk.
    c. While current\_npk-\>next\_npk \!= last\_npk:
    i. If current\_npk-\>marks\_npk \> current\_npk-\>next\_npk-\>marks\_npk (out of order):
    \* Swap the roll\_no, name, and marks data between current\_npk and current\_npk-\>next\_npk.
    \* Set swapped\_npk = true.
    ii. Move to the next node: current\_npk = current\_npk-\>next\_npk.
    d. Set last\_npk = current\_npk (The largest unsorted element is now at this position).
6.  End Do-While loop.
7.  End.

<!-- end list -->

````

---

##  C++ Code Implementation

```cpp
#include <iostream>
#include <string>
#include <cstdlib>
#include <limits> // Essential for std::numeric_limits

// --------------------- Node Structure ---------------------
struct student_npk {
    int roll_no_npk;
    std::string name_npk;
    float marks_npk;
    struct student_npk* prev_npk;
    struct student_npk* next_npk;
};

typedef struct student_npk DLL_npk;

// --------------------- Global Counter ---------------------
static int rollCounter_npk = 1;

// --------------------- Function Prototypes ---------------------
DLL_npk* getNode_npk();
DLL_npk* createList_npk();
void printList_npk(DLL_npk* head_npk);
void printListReverse_npk(DLL_npk* head_npk);
DLL_npk* insertAtBeginning_npk(DLL_npk* head_npk);
DLL_npk* insertAtEnd_npk(DLL_npk* head_npk);
DLL_npk* insertAfterRoll_npk(DLL_npk* head_npk, int targetRoll_npk);
DLL_npk* deleteAtBeginning_npk(DLL_npk* head_npk);
DLL_npk* deleteAtEnd_npk(DLL_npk* head_npk);
DLL_npk* deleteByRoll_npk(DLL_npk* head_npk, int roll_npk);
DLL_npk* searchByRoll_npk(DLL_npk* head_npk, int roll_npk);
int countNodes_npk(DLL_npk* head_npk);
DLL_npk* destroyList_npk(DLL_npk* head_npk);
void bubbleSort_npk(DLL_npk* head_npk);
void swapData_npk(DLL_npk* node1_npk, DLL_npk* node2_npk);


// --------------------- Menu Function (Corrected Input Handling) ---------------------
int menu_npk() {
    int choice_npk;
    std::cout << "\n========== Doubly Linked List Menu ==========\n";
    std::cout << "1. Create List\n";
    std::cout << "2. Print List (Head -> Tail)\n";
    std::cout << "3. Print List in Reverse (Tail -> Head)\n";
    std::cout << "4. Insert at Beginning\n";
    std::cout << "5. Insert at End\n";
    std::cout << "6. Insert After Specific Roll No\n";
    std::cout << "7. Delete at Beginning\n";
    std::cout << "8. Delete at End\n";
    std::cout << "9. Delete by Specific Roll No\n";
    std::cout << "10. Search by Roll No\n";
    std::cout << "11. Count Nodes\n";
    std::cout << "12. Destroy List\n";
    std::cout << "13. Bubble Sort by Marks\n"; 
    std::cout << "14. Exit\n";
    std::cout << "Enter your choice: ";
    
    // Fix for infinite loop: If cin fails (e.g., non-numeric input)...
    if (!(std::cin >> choice_npk)) {
        // 1. Clear the fail state.
        std::cin.clear();
        // 2. Discard all remaining characters in the input buffer.
        std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        return 0; // Return an invalid choice (handled by 'default' case in main)
    }
    return choice_npk;
}

// --------------------- Main Function ---------------------
int main() {
    DLL_npk* head_npk = nullptr;
    int choice_npk, roll_npk;

    while (true) {
        choice_npk = menu_npk();
        switch (choice_npk) {
        case 1: 
            head_npk = destroyList_npk(head_npk); // Destroy existing list first
            rollCounter_npk = 1; // Reset roll counter for new list
            head_npk = createList_npk(); 
            break;
        case 2: printList_npk(head_npk); break;
        case 3: printListReverse_npk(head_npk); break;
        case 4: head_npk = insertAtBeginning_npk(head_npk); break;
        case 5: head_npk = insertAtEnd_npk(head_npk); break;
        case 6:
            std::cout << "Enter roll no after which to insert: ";
            if (!(std::cin >> roll_npk)) {
                std::cin.clear(); std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
                std::cout << "Invalid input for roll number. Returning to menu.\n";
                break;
            }
            head_npk = insertAfterRoll_npk(head_npk, roll_npk);
            break;
        case 7: head_npk = deleteAtBeginning_npk(head_npk); break;
        case 8: head_npk = deleteAtEnd_npk(head_npk); break;
        case 9:
            std::cout << "Enter roll no to delete: ";
             if (!(std::cin >> roll_npk)) {
                std::cin.clear(); std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
                std::cout << "Invalid input for roll number. Returning to menu.\n";
                break;
            }
            head_npk = deleteByRoll_npk(head_npk, roll_npk);
            break;
        case 10:
            std::cout << "Enter roll no to search: ";
             if (!(std::cin >> roll_npk)) {
                std::cin.clear(); std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
                std::cout << "Invalid input for roll number. Returning to menu.\n";
                break;
            }
            searchByRoll_npk(head_npk, roll_npk);
            break;
        case 11:
            std::cout << "Total nodes = " << countNodes_npk(head_npk) << "\n";
            break;
        case 12:
            head_npk = destroyList_npk(head_npk);
            break;
        case 13: 
            bubbleSort_npk(head_npk);
            break;
        case 14:
            std::cout << "Exiting program...\n";
            destroyList_npk(head_npk); // Clean up memory before exit
            return 0;
        default:
            std::cout << "Invalid choice. Please enter a number from 1 to 14.\n";
        }
    }
    return 0;
}

// --------------------- Implementation Functions ---------------------
DLL_npk* getNode_npk() {
    // Standard practice: check for allocation failure
    DLL_npk* newNode_npk = new (std::nothrow) DLL_npk; 
    if (!newNode_npk) {
        std::cerr << "Memory allocation failed.\n";
        exit(1);
    }
    newNode_npk->prev_npk = nullptr;
    newNode_npk->next_npk = nullptr;
    return newNode_npk;
}

DLL_npk* createList_npk() {
    DLL_npk* head_npk = nullptr, * temp_npk = nullptr, * newNode_npk = nullptr;
    int choice_npk;
    std::cout << "--- Creating New List ---\n";
    while (true) {
        std::cout << "Add student? [1-Yes | 0-No]: ";
        if (!(std::cin >> choice_npk)) {
            std::cin.clear(); std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
            std::cout << "Invalid input. Stopping list creation.\n";
            break;
        }
        if (choice_npk == 0) break;
        
        newNode_npk = getNode_npk();
        newNode_npk->roll_no_npk = rollCounter_npk++;
        
        std::cout << "New Roll No: " << newNode_npk->roll_no_npk << "\n";
        std::cout << "Enter Name (single word): ";
        std::cin >> newNode_npk->name_npk;
        
        std::cout << "Enter Marks: ";
        if (!(std::cin >> newNode_npk->marks_npk)) {
            std::cin.clear(); std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
            std::cout << "Invalid marks input. Aborting current node creation.\n";
            delete newNode_npk; // Clean up the partially created node
            break; // Exit the list creation loop
        }
        
        if (!head_npk) head_npk = newNode_npk;
        else {
            temp_npk = head_npk;
            while (temp_npk->next_npk) temp_npk = temp_npk->next_npk;
            temp_npk->next_npk = newNode_npk;
            newNode_npk->prev_npk = temp_npk;
        }
    }
    std::cout << "List creation finished.\n";
    return head_npk;
}

void printList_npk(DLL_npk* head_npk) {
    if (!head_npk) {
        std::cout << "List is empty.\n";
        return;
    }
    std::cout << "--- List (Head -> Tail) ---\n";
    DLL_npk* current_npk = head_npk;
    while (current_npk != nullptr) {
        std::cout << "Roll: " << current_npk->roll_no_npk
                  << " | Name: " << current_npk->name_npk
                  << " | Marks: " << current_npk->marks_npk << "\n";
        current_npk = current_npk->next_npk;
    }
}

void printListReverse_npk(DLL_npk* head_npk) {
    if (!head_npk) {
        std::cout << "List is empty.\n";
        return;
    }
    std::cout << "--- List (Tail -> Head) ---\n";
    DLL_npk* temp_npk = head_npk;
    // Find the tail
    while (temp_npk->next_npk) temp_npk = temp_npk->next_npk;
    
    // Print in reverse
    while (temp_npk != nullptr) {
        std::cout << "Roll: " << temp_npk->roll_no_npk
                  << " | Name: " << temp_npk->name_npk
                  << " | Marks: " << temp_npk->marks_npk << "\n";
        temp_npk = temp_npk->prev_npk;
    }
}

DLL_npk* insertAtBeginning_npk(DLL_npk* head_npk) {
    DLL_npk* newNode_npk = getNode_npk();
    newNode_npk->roll_no_npk = rollCounter_npk++;
    std::cout << "Enter Name (single word): ";
    std::cin >> newNode_npk->name_npk;
    std::cout << "Enter Marks: ";
    if (!(std::cin >> newNode_npk->marks_npk)) {
        std::cin.clear(); std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        std::cout << "Invalid marks input. Insertion aborted.\n";
        delete newNode_npk;
        return head_npk;
    }
    
    newNode_npk->next_npk = head_npk;
    if (head_npk) head_npk->prev_npk = newNode_npk;
    std::cout << "Student with Roll " << newNode_npk->roll_no_npk << " inserted at beginning.\n";
    return newNode_npk;
}

DLL_npk* insertAtEnd_npk(DLL_npk* head_npk) {
    DLL_npk* newNode_npk = getNode_npk();
    newNode_npk->roll_no_npk = rollCounter_npk++;
    std::cout << "Enter Name (single word): ";
    std::cin >> newNode_npk->name_npk;
    std::cout << "Enter Marks: ";
    if (!(std::cin >> newNode_npk->marks_npk)) {
        std::cin.clear(); std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        std::cout << "Invalid marks input. Insertion aborted.\n";
        delete newNode_npk;
        return head_npk;
    }
    
    if (!head_npk) {
        std::cout << "Student with Roll " << newNode_npk->roll_no_npk << " inserted (list was empty).\n";
        return newNode_npk;
    }
    DLL_npk* temp_npk = head_npk;
    while (temp_npk->next_npk) temp_npk = temp_npk->next_npk;
    temp_npk->next_npk = newNode_npk;
    newNode_npk->prev_npk = temp_npk;
    std::cout << "Student with Roll " << newNode_npk->roll_no_npk << " inserted at end.\n";
    return head_npk;
}

DLL_npk* insertAfterRoll_npk(DLL_npk* head_npk, int targetRoll_npk) {
    if (!head_npk) {
        std::cout << "List is empty, cannot insert after roll.\n";
        return nullptr;
    }
    DLL_npk* temp_npk = head_npk;
    while (temp_npk && temp_npk->roll_no_npk != targetRoll_npk) temp_npk = temp_npk->next_npk;
    if (!temp_npk) {
        std::cout << "Roll " << targetRoll_npk << " not found. Insertion aborted.\n";
        return head_npk;
    }
    
    DLL_npk* newNode_npk = getNode_npk();
    newNode_npk->roll_no_npk = rollCounter_npk++;
    std::cout << "Enter Name (single word): ";
    std::cin >> newNode_npk->name_npk;
    std::cout << "Enter Marks: ";
    if (!(std::cin >> newNode_npk->marks_npk)) {
        std::cin.clear(); std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        std::cout << "Invalid marks input. Insertion aborted.\n";
        delete newNode_npk;
        return head_npk;
    }
    
    newNode_npk->next_npk = temp_npk->next_npk;
    newNode_npk->prev_npk = temp_npk;
    if (temp_npk->next_npk) temp_npk->next_npk->prev_npk = newNode_npk;
    temp_npk->next_npk = newNode_npk;
    std::cout << "Student with Roll " << newNode_npk->roll_no_npk << " inserted after Roll " << targetRoll_npk << ".\n";
    return head_npk;
}

DLL_npk* deleteAtBeginning_npk(DLL_npk* head_npk) {
    if (!head_npk) {
        std::cout << "List is empty. Cannot delete.\n";
        return nullptr;
    }
    DLL_npk* temp_npk = head_npk;
    head_npk = head_npk->next_npk;
    if (head_npk) head_npk->prev_npk = nullptr;
    std::cout << "Deleted student with Roll: " << temp_npk->roll_no_npk << " (at beginning).\n";
    delete temp_npk;
    return head_npk;
}

DLL_npk* deleteAtEnd_npk(DLL_npk* head_npk) {
    if (!head_npk) {
        std::cout << "List is empty. Cannot delete.\n";
        return nullptr;
    }
    
    DLL_npk* temp_npk = head_npk;
    if (!temp_npk->next_npk) { // Only one node
        std::cout << "Deleted student with Roll: " << temp_npk->roll_no_npk << " (only node).\n";
        delete temp_npk;
        return nullptr;
    }
    
    while (temp_npk->next_npk) temp_npk = temp_npk->next_npk; // Find the last node
    
    temp_npk->prev_npk->next_npk = nullptr;
    std::cout << "Deleted student with Roll: " << temp_npk->roll_no_npk << " (at end).\n";
    delete temp_npk;
    return head_npk;
}

DLL_npk* deleteByRoll_npk(DLL_npk* head_npk, int roll_npk) {
    if (!head_npk) {
        std::cout << "List is empty. Cannot delete.\n";
        return nullptr;
    }
    
    DLL_npk* temp_npk = head_npk;
    while (temp_npk && temp_npk->roll_no_npk != roll_npk) temp_npk = temp_npk->next_npk;
    
    if (!temp_npk) {
        std::cout << "Roll " << roll_npk << " not found.\n";
        return head_npk;
    }
    
    if (temp_npk->prev_npk) temp_npk->prev_npk->next_npk = temp_npk->next_npk;
    else head_npk = temp_npk->next_npk; // Deleting the head
    
    if (temp_npk->next_npk) temp_npk->next_npk->prev_npk = temp_npk->prev_npk;
    
    std::cout << "Deleted student with Roll: " << temp_npk->roll_no_npk << ".\n";
    delete temp_npk;
    return head_npk;
}

DLL_npk* searchByRoll_npk(DLL_npk* head_npk, int roll_npk) {
    if (!head_npk) {
        std::cout << "List is empty.\n";
        return nullptr;
    }
    
    DLL_npk* current_npk = head_npk;
    while (current_npk) {
        if (current_npk->roll_no_npk == roll_npk) {
            std::cout << "Found: Roll: " << current_npk->roll_no_npk
                      << " | Name: " << current_npk->name_npk
                      << " | Marks: " << current_npk->marks_npk << "\n";
            return current_npk;
        }
        current_npk = current_npk->next_npk;
    }
    std::cout << "Roll " << roll_npk << " not found.\n";
    return nullptr;
}

int countNodes_npk(DLL_npk* head_npk) {
    int count_npk = 0;
    DLL_npk* current_npk = head_npk;
    while (current_npk) {
        count_npk++;
        current_npk = current_npk->next_npk;
    }
    return count_npk;
}

DLL_npk* destroyList_npk(DLL_npk* head_npk) {
    if (!head_npk) return nullptr;
    
    DLL_npk* temp_npk;
    while (head_npk) {
        temp_npk = head_npk;
        head_npk = head_npk->next_npk;
        delete temp_npk;
    }
    std::cout << "List destroyed and all memory freed.\n";
    return nullptr;
}

void swapData_npk(DLL_npk* node1_npk, DLL_npk* node2_npk) {
    // Swapping the data fields is simpler for Bubble Sort implementation in a DLL
    int tempRoll_npk = node1_npk->roll_no_npk;
    std::string tempName_npk = node1_npk->name_npk;
    float tempMarks_npk = node1_npk->marks_npk;

    node1_npk->roll_no_npk = node2_npk->roll_no_npk;
    node1_npk->name_npk = node2_npk->name_npk;
    node1_npk->marks_npk = node2_npk->marks_npk;

    node2_npk->roll_no_npk = tempRoll_npk;
    node2_npk->name_npk = tempName_npk;
    node2_npk->marks_npk = tempMarks_npk;
}

void bubbleSort_npk(DLL_npk* head_npk) {
    if (!head_npk || !head_npk->next_npk) {
        std::cout << "List is empty or has only one node, sorting not required.\n";
        return;
    }

    bool swapped_npk;
    DLL_npk* current_npk;
    DLL_npk* last_npk = nullptr;

    do {
        swapped_npk = false;
        current_npk = head_npk;

        while (current_npk->next_npk != last_npk) {
            // Sort by Marks in ascending order
            if (current_npk->marks_npk > current_npk->next_npk->marks_npk) {
                swapData_npk(current_npk, current_npk->next_npk);
                swapped_npk = true;
            }
            current_npk = current_npk->next_npk;
        }
        // After each pass, the last node checked is sorted
        last_npk = current_npk; 
    } while (swapped_npk);

    std::cout << "List sorted by Marks (ascending) using Bubble Sort.\n";
}

````

-----

##  Output
```

PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_18.cpp -o Assign_18 } ; if ($?) { .\Assign_18 }

========== Doubly Linked List Menu ==========
1. Create List
2. Print List (Head -> Tail)
3. Print List in Reverse (Tail -> Head)
4. Insert at Beginning
5. Insert at End
6. Insert After Specific Roll No
7. Delete at Beginning
8. Delete at End
9. Delete by Specific Roll No
10. Search by Roll No
11. Count Nodes
12. Destroy List
13. Bubble Sort by Marks
14. Exit
Enter your choice: 1
--- Creating New List ---
Add student? [1-Yes | 0-No]: 1
New Roll No: 1
Enter Name (single word): Nandini
Enter Marks: 100
Add student? [1-Yes | 0-No]: 1
New Roll No: 2
Enter Name (single word): Ram
Enter Marks: 99
Add student? [1-Yes | 0-No]: 0
List creation finished.

========== Doubly Linked List Menu ==========
1. Create List
2. Print List (Head -> Tail)
3. Print List in Reverse (Tail -> Head)
4. Insert at Beginning
5. Insert at End
6. Insert After Specific Roll No
7. Delete at Beginning
8. Delete at End
9. Delete by Specific Roll No
10. Search by Roll No
11. Count Nodes
12. Destroy List
13. Bubble Sort by Marks
14. Exit
Enter your choice: 11
Total nodes = 2

========== Doubly Linked List Menu ==========
1. Create List
2. Print List (Head -> Tail)
3. Print List in Reverse (Tail -> Head)
4. Insert at Beginning
5. Insert at End
6. Insert After Specific Roll No
7. Delete at Beginning
8. Delete at End
9. Delete by Specific Roll No
10. Search by Roll No
11. Count Nodes
12. Destroy List
13. Bubble Sort by Marks
14. Exit
Enter your choice:

````