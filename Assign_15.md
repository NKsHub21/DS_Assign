## ASSIGNMENT NO - 5 Unit_2

\<p align="center"\>Binary Number Operations using Doubly Linked List (DLL)\</p\>

-----

## Concept: Representing Binary Numbers with DLL

A **Doubly Linked List (DLL)** is an ideal structure for representing binary numbers because:

1.  **Arbitrary Length:** It can store binary numbers of any length, unlike fixed-size data types (like `int` or `long`).
2.  **Bi-directional Access:** The `prev` pointer is crucial for performing arithmetic operations (like addition), which often require moving from the **Least Significant Bit (LSB) to the Most Significant Bit (MSB)**, i.e., from tail to head.

Each node in the DLL stores a single **bit** (0 or 1).

-----

## Algorithms

### A) Complement Operations

#### 1\. 1's Complement

Traverse the binary number DLL from the **head** to the **tail**. For every node encountered:

  * If the bit is **0**, change it to **1**.
  * If the bit is **1**, change it to **0**.
  * Display the result bit-by-bit.

#### 2\. 2's Complement

Calculate the 2's complement by performing the **1's complement and then adding 1** to the result.

1.  **1's Complement:** As described above.
2.  **Add 1:**
      * Start traversing the **1's complement DLL** from the **tail (LSB)**.
      * Find the **first '0' from the right**.
      * Change this '0' to **1**.
      * Change all the preceding '1's (to the right of the found '0') to **0**.
      * If no '0' is found (the number is all '1's), change all '1's to '0's and prepend a new node with '1' to the head.

-----

### B) Binary Addition

1.  **Initialization:** Initialize a `carry_npk` variable to 0. The result will be stored in a new DLL (`headR_npk`).

2.  **Alignment:** Identify the tails of the two input DLLs (`tail1_npk`, `tail2_npk`). Start the traversal from the tail (LSB) of both lists.

3.  **Iteration (Tail to Head):** Loop while either list still has nodes OR `carry_npk` is 1.

      * Get the current bits: `bit1_npk` (from `tail1_npk`) and `bit2_npk` (from `tail2_npk`). If a list is exhausted, its bit is 0.
      * Calculate the `sum_npk` using the current bits and `carry_npk`.
      * $Sum = \text{bit1} \oplus \text{bit2} \oplus \text{carry}$
      * $Carry_{new} = (\text{bit1} \cdot \text{bit2}) + (\text{bit1} \cdot \text{carry}) + (\text{bit2} \cdot \text{carry})$
      * Insert the `sum_npk` bit at the **beginning** of the result list (`headR_npk`).
      * Move to the previous node in both input lists (`tail->prev_npk`).

4.  **Final Carry:** If a final carry (1) remains after the loop, insert a new node with '1' at the beginning of the result list.

-----

## C++ Code Implementation

```cpp
#include <iostream>
#include <cstdlib>
#include <cstring>
#include <algorithm> // For max

using namespace std;

// --------------------- Node Structure ---------------------
typedef struct binaryBit_npk {
    int bit_npk; // Stores 0 or 1
    struct binaryBit_npk* prev_npk;
    struct binaryBit_npk* next_npk;
} DLL_npk;

// --------------------- Function Prototypes ---------------------
DLL_npk* getNode_npk(int bit_npk);
DLL_npk* createBinaryList_npk();
void displayBinary_npk(DLL_npk* head_npk);
DLL_npk* copyList_npk(DLL_npk* head_npk);
DLL_npk* destroyList_npk(DLL_npk* head_npk);
DLL_npk* getTail_npk(DLL_npk* head_npk);

// A) Complement Operations
DLL_npk* onesComplement_npk(DLL_npk* head_npk);
DLL_npk* twosComplement_npk(DLL_npk* head_npk);

// B) Binary Addition
DLL_npk* addBinary_npk(DLL_npk* head1_npk, DLL_npk* head2_npk);

// --------------------- Main Function ---------------------
int menu_npk() {
    int choice_npk;
    cout << "\n========== Binary Number DLL Operations ==========\n";
    cout << "1. Create Binary Number\n";
    cout << "2. Display Binary Number\n";
    cout << "3. Calculate 1's Complement\n";
    cout << "4. Calculate 2's Complement\n";
    cout << "5. Perform Binary Addition (Requires two lists)\n";
    cout << "6. Exit\n";
    cout << "Enter your choice: ";
    cin >> choice_npk;
    return choice_npk;
}

int main() {
    DLL_npk* head1_npk = NULL;
    DLL_npk* head2_npk = NULL;
    DLL_npk* result_npk = NULL;
    int choice_npk;

    while (1) {
        choice_npk = menu_npk();
        switch (choice_npk) {
        case 1:
            if (head1_npk) destroyList_npk(head1_npk);
            head1_npk = createBinaryList_npk();
            break;
        case 2:
            displayBinary_npk(head1_npk);
            break;
        case 3:
            result_npk = onesComplement_npk(head1_npk);
            cout << "1's Complement: ";
            displayBinary_npk(result_npk);
            destroyList_npk(result_npk);
            break;
        case 4:
            result_npk = twosComplement_npk(head1_npk);
            cout << "2's Complement: ";
            displayBinary_npk(result_npk);
            destroyList_npk(result_npk);
            break;
        case 5:
            cout << "--- Creating First Binary Number ---\n";
            if (head1_npk) destroyList_npk(head1_npk);
            head1_npk = createBinaryList_npk();
            cout << "--- Creating Second Binary Number ---\n";
            if (head2_npk) destroyList_npk(head2_npk);
            head2_npk = createBinaryList_npk();
            
            result_npk = addBinary_npk(head1_npk, head2_npk);
            cout << "Result of Addition: ";
            displayBinary_npk(result_npk);
            destroyList_npk(result_npk);
            break;
        case 6:
            cout << "Exiting program...\n";
            destroyList_npk(head1_npk);
            destroyList_npk(head2_npk);
            exit(0);
        default:
            cout << "Invalid choice.\n";
        }
    }
    return 0;
}

// --------------------- Utility Functions ---------------------

DLL_npk* getNode_npk(int bit_npk) {
    DLL_npk* newNode_npk = new DLL_npk;
    if (!newNode_npk) {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    newNode_npk->bit_npk = bit_npk;
    newNode_npk->prev_npk = NULL;
    newNode_npk->next_npk = NULL;
    return newNode_npk;
}

DLL_npk* createBinaryList_npk() {
    DLL_npk* head_npk = NULL, * temp_npk = NULL;
    int choice_npk, bit_npk;
    
    cout << "Enter binary number bit by bit (MSB first):\n";
    while (1) {
        cout << "Enter bit [0/1] or -1 to stop: ";
        cin >> bit_npk;
        if (bit_npk == -1) break;
        if (bit_npk != 0 && bit_npk != 1) {
            cout << "Invalid bit. Enter 0 or 1.\n";
            continue;
        }

        DLL_npk* newNode_npk = getNode_npk(bit_npk);
        if (!head_npk) {
            head_npk = newNode_npk;
        } else {
            temp_npk = head_npk;
            while (temp_npk->next_npk) temp_npk = temp_npk->next_npk;
            temp_npk->next_npk = newNode_npk;
            newNode_npk->prev_npk = temp_npk;
        }
    }
    return head_npk;
}

void displayBinary_npk(DLL_npk* head_npk) {
    if (!head_npk) {
        cout << "[]\n";
        return;
    }
    DLL_npk* temp_npk = head_npk;
    cout << "Binary: ";
    while (temp_npk) {
        cout << temp_npk->bit_npk;
        temp_npk = temp_npk->next_npk;
    }
    cout << "\n";
}

// Get the last node (LSB) - necessary for arithmetic
DLL_npk* getTail_npk(DLL_npk* head_npk) {
    if (!head_npk) return NULL;
    DLL_npk* temp_npk = head_npk;
    while (temp_npk->next_npk) {
        temp_npk = temp_npk->next_npk;
    }
    return temp_npk;
}

// Deep copy of a list
DLL_npk* copyList_npk(DLL_npk* head_npk) {
    if (!head_npk) return NULL;
    DLL_npk* newHead_npk = NULL;
    DLL_npk* newTail_npk = NULL;
    DLL_npk* current_npk = head_npk;

    while (current_npk) {
        DLL_npk* newNode_npk = getNode_npk(current_npk->bit_npk);
        if (!newHead_npk) {
            newHead_npk = newNode_npk;
            newTail_npk = newNode_npk;
        } else {
            newTail_npk->next_npk = newNode_npk;
            newNode_npk->prev_npk = newTail_npk;
            newTail_npk = newNode_npk;
        }
        current_npk = current_npk->next_npk;
    }
    return newHead_npk;
}

DLL_npk* destroyList_npk(DLL_npk* head_npk) {
    DLL_npk* temp_npk;
    while (head_npk) {
        temp_npk = head_npk;
        head_npk = head_npk->next_npk;
        delete temp_npk;
    }
    return NULL;
}

// --------------------- A) Complement Operations ---------------------

/* Calculate and display the 1’s complement */
DLL_npk* onesComplement_npk(DLL_npk* head_npk) {
    if (!head_npk) {
        cout << "Error: List is empty.\n";
        return NULL;
    }
    DLL_npk* result_npk = copyList_npk(head_npk);
    DLL_npk* temp_npk = result_npk;

    while (temp_npk) {
        temp_npk->bit_npk = 1 - temp_npk->bit_npk;
        temp_npk = temp_npk->next_npk;
    }
    return result_npk;
}

/* Calculate and display the 2’s complement */
DLL_npk* twosComplement_npk(DLL_npk* head_npk) {
    if (!head_npk) {
        cout << "Error: List is empty.\n";
        return NULL;
    }

    // Step 1: Get 1's complement
    DLL_npk* comp1_npk = onesComplement_npk(head_npk);
    if (!comp1_npk) return NULL;
    
    // Step 2: Add 1 to 1's complement (Start from LSB)
    DLL_npk* current_npk = getTail_npk(comp1_npk);
    int carry_npk = 1;

    // Traverse from LSB to MSB
    while (current_npk && carry_npk) {
        int sum_npk = current_npk->bit_npk + carry_npk;
        current_npk->bit_npk = sum_npk % 2;
        carry_npk = sum_npk / 2;
        current_npk = current_npk->prev_npk;
    }
    
    // Step 3: Handle final carry (if number was all 1s, e.g., 111 -> 000 + 1)
    if (carry_npk) {
        DLL_npk* newHead_npk = getNode_npk(1);
        newHead_npk->next_npk = comp1_npk;
        comp1_npk->prev_npk = newHead_npk;
        return newHead_npk;
    }

    return comp1_npk;
}

// --------------------- B) Binary Addition ---------------------

/* Perform addition of two binary numbers */
DLL_npk* addBinary_npk(DLL_npk* head1_npk, DLL_npk* head2_npk) {
    if (!head1_npk && !head2_npk) return NULL;
    
    DLL_npk* tail1_npk = getTail_npk(head1_npk);
    DLL_npk* tail2_npk = getTail_npk(head2_npk);
    
    DLL_npk* resultHead_npk = NULL;
    int carry_npk = 0;
    int sum_npk;

    while (tail1_npk || tail2_npk || carry_npk) {
        int bit1_npk = (tail1_npk) ? tail1_npk->bit_npk : 0;
        int bit2_npk = (tail2_npk) ? tail2_npk->bit_npk : 0;
        
        // Sum and new carry calculation
        sum_npk = bit1_npk ^ bit2_npk ^ carry_npk; // XOR gives the result bit
        carry_npk = (bit1_npk & bit2_npk) | (bit1_npk & carry_npk) | (bit2_npk & carry_npk); // Majority function for carry

        // Insert the sum bit at the beginning of the result list (since we traverse LSB to MSB)
        DLL_npk* newNode_npk = getNode_npk(sum_npk);
        newNode_npk->next_npk = resultHead_npk;
        if (resultHead_npk) {
            resultHead_npk->prev_npk = newNode_npk;
        }
        resultHead_npk = newNode_npk;

        // Move to the next most significant bit
        if (tail1_npk) tail1_npk = tail1_npk->prev_npk;
        if (tail2_npk) tail2_npk = tail2_npk->prev_npk;
    }

    return resultHead_npk;
}
```

-----

## Output

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_15.cpp -o Assign_15 } ; if ($?) { .\Assign_15 }

========== Binary Number DLL Operations ==========
1. Create Binary Number
2. Display Binary Number
3. Calculate 1's Complement
4. Calculate 2's Complement
5. Perform Binary Addition (Requires two lists)
6. Exit
Enter your choice: 1
Enter binary number bit by bit (MSB first):
Enter bit [0/1] or -1 to stop: 1111
Invalid bit. Enter 0 or 1.
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: 0
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: -1

========== Binary Number DLL Operations ==========
1. Create Binary Number
2. Display Binary Number
3. Calculate 1's Complement
4. Calculate 2's Complement
5. Perform Binary Addition (Requires two lists)
6. Exit
Enter your choice: 2
Binary: 111101

========== Binary Number DLL Operations ==========
1. Create Binary Number
2. Display Binary Number
3. Calculate 1's Complement
4. Calculate 2's Complement
5. Perform Binary Addition (Requires two lists)
6. Exit
Enter your choice: 4
2's Complement: Binary: 000011

========== Binary Number DLL Operations ==========
1. Create Binary Number
2. Display Binary Number
3. Calculate 1's Complement
4. Calculate 2's Complement
5. Perform Binary Addition (Requires two lists)
6. Exit
Enter your choice: 5
--- Creating First Binary Number ---
Enter binary number bit by bit (MSB first):
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: -1
--- Creating Second Binary Number ---
Enter binary number bit by bit (MSB first):
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: 1
Enter bit [0/1] or -1 to stop: 0
Enter bit [0/1] or -1 to stop: -1
Result of Addition: Binary: 11101

========== Binary Number DLL Operations ==========
1. Create Binary Number
2. Display Binary Number
3. Calculate 1's Complement
4. Calculate 2's Complement
5. Perform Binary Addition (Requires two lists)
6. Exit
Enter your choice:
```