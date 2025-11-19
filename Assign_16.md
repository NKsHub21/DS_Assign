## ASSIGNMENT: 6 Unit_2 SET IMPLEMENTATION USING GENERALIZED LINKED LIST (GLL)

<p align="center">Implementation of a Nested Set Structure using Generalized Linked List (GLL)</p>

---

## Concept: Generalized Linked List (GLL)

A **Generalized Linked List (GLL)** is a recursive data structure where nodes can hold either a simple data element or a pointer to another sublist (which is itself a GLL). This structure is essential for representing multi-dimensional, nested, or hierarchical data like **sets within sets** or algebraic expressions.

Each node (`GNode_npk`) in this implementation contains:

1.  **`flag_npk` Field:** An integer indicating the node type:
    * `0`: Data Node (stores a simple element, e.g., 'p').
    * `1`: Sublist Node (stores a pointer to another GLL, e.g., `\{r, s, t, ...\}`).
2.  **`data_npk` Field:** Stores the simple character element (used only if `flag_npk` is `0`).
3.  **`sublist_npk` Pointer:** Points to the **DUMMY HEAD** of a nested sublist (used only if `flag_npk` is `1`).
4.  **`next_npk` Pointer:** Points to the next node at the same level in the current list.

**Note on Dummy Heads:** Each list, including the main set and every sublist, is managed by a **Dummy Head** node. This simplifies list manipulation as the actual data starts at `head->next_npk`.

---

## Set Structure Represented

The program implements the Generalized Linked List for the following specific nested set:

$$ S = \{ p, q, \{r, s, t, \{\}, \{u, v\}, w, x, \{y, z\}, a1, b1\}, a1, b1 \} $$

| **Original Element** | **GLL Node Type** | **Representation in Code** |
| :--- | :--- | :--- |
| `p`, `q` (Outer) | Data Node (`flag_npk=0`) | Character data: `'p'`, `'q'` |
| `{r, s, t, ...}` | Sublist Node (`flag_npk=1`) | Pointer to the DUMMY HEAD of Sublist A |
| `\{\}` (Empty Set) | Sublist Node (`flag_npk=1`) | Pointer to the DUMMY HEAD of Sublist B (with `next_npk=NULL`) |
| `a1`, `b1` (Outer) | Data Node (`flag_npk=0`) | Character data: `'A'`, `'B'` (mapped due to `char` limitation) |

---

## Algorithms

The implementation is entirely recursive, leveraging the hierarchical nature of the GLL.

### 1. `getNewNode_npk()`

* **Goal:** Allocate and initialize a single GLL node.
* **Summary:** Uses `new (std::nothrow) GLL_npk` for memory allocation. Initializes `next_npk` and `sublist_npk` to `nullptr`.

### 2. `constructSetS_npk()`

* **Goal:** Build the specific structure of set $S$ using hardcoded links.
* **Summary:** Creates all necessary GLLs (Sublist B: `\{\}`, Sublist C: `\{u, v\}`, Sublist D: `\{y, z\}`, Sublist A, and the main Set S) by sequentially allocating nodes, setting `flag_npk` (0 or 1), and linking them via `next_npk`.

### 3. `displaySet_npk(head_npk)`

* **Goal:** Recursively print the set in correct set notation (e.g., `{element, {sublist}, ...}`).
* **Summary:**
    1. Prints the opening brace `{`.
    2. Starts iteration from `head_npk->next_npk` (skipping the Dummy Head).
    3. If `flag_npk == 0` (Data Node), prints the element (`data_npk`).
    4. If `flag_npk == 1` (Sublist Node), it **recursively calls** `displaySet_npk(temp_npk->sublist_npk)` to handle the nested list.
    5. Prints the closing brace `}` after traversing all elements at the current level.

### 4. `destroyGLL_npk(head_npk)`

* **Goal:** Recursively deallocate all memory used by the list structure.
* **Summary:** Traverses the list. If a Sublist Node (`flag_npk=1`) is encountered, it **recursively calls** `destroyGLL_npk` on the `sublist_npk` pointer (the dummy head of the nested list) before using `delete` on the current node. Finally, it deletes the initial `head_npk` (Dummy Head).

---

## C++ Code Implementation

```cpp:Generalized Linked List Set Implementation:set_gll_implementation_npk.cpp
#include <iostream>
#include <cstdlib> // For exit()

// Define the structure for a GLL node, based on the provided C reference
struct GNode_npk {
    int flag_npk;               // 0 = data, 1 = sublist
    char data_npk;              // used only if flag_npk == 0
    GNode_npk* sublist_npk;      // points to DUMMY HEAD of sublist if flag_npk == 1
    GNode_npk* next_npk;         // next node (same level)
};

// Use a typedef for convenience
typedef GNode_npk GLL_npk;

// ------------------------------------------------------
// Function: getNewNode_npk()
// Allocates memory for a node and initializes pointers.
// ------------------------------------------------------
GLL_npk* getNewNode_npk(void) {
    GLL_npk* node_npk = new (std::nothrow) GLL_npk;
    if (!node_npk) {
        std::cerr << "Memory allocation failed_npk." << std::endl;
        exit(EXIT_FAILURE);
    }
    node_npk->next_npk = nullptr;
    node_npk->sublist_npk = nullptr;
    return node_npk;
}

// ------------------------------------------------------
// Function: createDataNode_npk(char data_char_npk)
// Helper to create a node holding single character data.
// ------------------------------------------------------
GLL_npk* createDataNode_npk(char data_char_npk) {
    GLL_npk* newNode_npk = getNewNode_npk();
    newNode_npk->flag_npk = 0;
    newNode_npk->data_npk = data_char_npk;
    return newNode_npk;
}

// ------------------------------------------------------
// Function: createSublistNode_npk(GLL_npk* sublist_head_npk)
// Helper to create a node holding a sublist pointer.
// ------------------------------------------------------
GLL_npk* createSublistNode_npk(GLL_npk* sublist_head_npk) {
    GLL_npk* newNode_npk = getNewNode_npk();
    newNode_npk->flag_npk = 1;
    newNode_npk->sublist_npk = sublist_head_npk;
    return newNode_npk;
}

// ------------------------------------------------------
// Function: destroyGLL_npk(head_npk)
// Recursively frees all memory starting from the DUMMY head.
// ------------------------------------------------------
void destroyGLL_npk(GLL_npk* head_npk) {
    if (!head_npk) return;

    GLL_npk* temp_npk = head_npk->next_npk;
    while (temp_npk != nullptr) {
        GLL_npk* nextNode_npk = temp_npk->next_npk;
        if (temp_npk->flag_npk == 1) {
            // Recursively destroy the sublist (which starts with a DUMMY head)
            destroyGLL_npk(temp_npk->sublist_npk);
        }
        delete temp_npk;
        temp_npk = nextNode_npk;
    }
    // Finally, free the DUMMY head itself
    delete head_npk;
}

// ------------------------------------------------------
// Function: displaySet_npk(head_npk)
// Recursively prints the GLL in correct set notation {..., {..., ...}, ...}
// This function assumes the input 'head_npk' is a DUMMY head.
// ------------------------------------------------------
void displaySet_npk(GLL_npk* head_npk) {
    // Start of the set notation: {
    std::cout << "{";

    GLL_npk* temp_npk = head_npk->next_npk; // Start from the first actual element, skipping DUMMY
    bool isFirst_npk = true;

    while (temp_npk != nullptr) {
        if (!isFirst_npk) {
            // Print comma separator for all elements after the first one
            std::cout << ", ";
        }

        if (temp_npk->flag_npk == 0) {
            // Data node: print the character
            std::cout << temp_npk->data_npk;
        } else {
            // Sublist node: Recursively call the display function
            // Pass the sublist's DUMMY head
            displaySet_npk(temp_npk->sublist_npk);
        }

        isFirst_npk = false;
        temp_npk = temp_npk->next_npk;
    }

    // End of the set notation: }
    std::cout << "}";
}

// ------------------------------------------------------
// Function: constructSetS_npk()
// Hardcodes the creation of the specific set S
// ------------------------------------------------------
GLL_npk* constructSetS_npk() {
    // NOTE: The GLL structure only supports single 'char' data. 
    // We map two-character labels (a1, b1) to single chars for implementation:
    // a1 (outer) -> 'A', b1 (outer) -> 'B'
    // a1 (inner) -> 'a', b1 (inner) -> 'b'

    // --- Sublist D: {y, z} ---
    GLL_npk* headD_npk = getNewNode_npk();
    GLL_npk* tempD_npk = headD_npk;
    tempD_npk->next_npk = createDataNode_npk('y'); tempD_npk = tempD_npk->next_npk;
    tempD_npk->next_npk = createDataNode_npk('z'); tempD_npk = tempD_npk->next_npk;

    // --- Sublist C: {u, v} ---
    GLL_npk* headC_npk = getNewNode_npk();
    GLL_npk* tempC_npk = headC_npk;
    tempC_npk->next_npk = createDataNode_npk('u'); tempC_npk = tempC_npk->next_npk;
    tempC_npk->next_npk = createDataNode_npk('v'); tempC_npk = tempC_npk->next_npk;

    // --- Sublist B: {} (Empty Set) ---
    GLL_npk* headB_npk = getNewNode_npk(); // DUMMY head with next_npk = nullptr (already set)

    // --- Sublist A: {r, s, t, {}, {u, v}, w, x, {y, z}, a, b} ---
    GLL_npk* headA_npk = getNewNode_npk();
    GLL_npk* tempA_npk = headA_npk;

    tempA_npk->next_npk = createDataNode_npk('r'); tempA_npk = tempA_npk->next_npk;
    tempA_npk->next_npk = createDataNode_npk('s'); tempA_npk = tempA_npk->next_npk;
    tempA_npk->next_npk = createDataNode_npk('t'); tempA_npk = tempA_npk->next_npk;
    
    // Node for Sublist B: {}
    tempA_npk->next_npk = createSublistNode_npk(headB_npk); tempA_npk = tempA_npk->next_npk;

    // Node for Sublist C: {u, v}
    tempA_npk->next_npk = createSublistNode_npk(headC_npk); tempA_npk = tempA_npk->next_npk;

    tempA_npk->next_npk = createDataNode_npk('w'); tempA_npk = tempA_npk->next_npk;
    tempA_npk->next_npk = createDataNode_npk('x'); tempA_npk = tempA_npk->next_npk;

    // Node for Sublist D: {y, z}
    tempA_npk->next_npk = createSublistNode_npk(headD_npk); tempA_npk = tempA_npk->next_npk;

    // Inner a1, b1
    tempA_npk->next_npk = createDataNode_npk('a'); tempA_npk = tempA_npk->next_npk; // 'a1' -> 'a'
    tempA_npk->next_npk = createDataNode_npk('b'); tempA_npk = tempA_npk->next_npk; // 'b1' -> 'b'

    // --- Main Set S: {p, q, Sublist A, A, B} ---
    GLL_npk* headS_npk = getNewNode_npk(); // DUMMY head for S
    GLL_npk* tempS_npk = headS_npk;

    tempS_npk->next_npk = createDataNode_npk('p'); tempS_npk = tempS_npk->next_npk;
    tempS_npk->next_npk = createDataNode_npk('q'); tempS_npk = tempS_npk->next_npk;

    // Node for Sublist A
    tempS_npk->next_npk = createSublistNode_npk(headA_npk); tempS_npk = tempS_npk->next_npk;

    // Outer a1, b1
    tempS_npk->next_npk = createDataNode_npk('A'); tempS_npk = tempS_npk->next_npk; // 'a1' -> 'A'
    tempS_npk->next_npk = createDataNode_npk('B'); tempS_npk = tempS_npk->next_npk; // 'b1' -> 'B'

    return headS_npk;
}

// ------------------------------------------------------
// Main Function
// The name is changed to 'main' from 'main_npk' to fix the
// "undefined reference to WinMain" linker error in MinGW.
// ------------------------------------------------------
int main(void) {
    std::cout << "Starting Generalized Linked List (GLL) Set Implementation_npk." << std::endl;

    // 1. Construct the GLL representing the set S
    std::cout << "Constructing GLL for set S_npk..." << std::endl;
    GLL_npk* setS_head_npk = constructSetS_npk();
    
    // 2. Display the elements in correct set notation
    std::cout << "\nSet S in GLL format is: " << std::endl;
    std::cout << "S = ";
    displaySet_npk(setS_head_npk);
    std::cout << "\n\n(Note: Two-character labels 'a1', 'b1' were mapped to single characters 'A', 'B', 'a', 'b' due to node structure limitations.)\n" << std::endl;

    // 3. Cleanup
    std::cout << "Destroying GLL and freeing memory_npk..." << std::endl;
    destroyGLL_npk(setS_head_npk);
    std::cout << "Cleanup complete_npk." << std::endl;

    return 0;
}
```eof

---

##Output

```

PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_16.cpp -o Assign_16 } ; if ($?) { .\Assign_16 }
Starting Generalized Linked List (GLL) Set Implementation_npk.
Constructing GLL for set S_npk...

Set S in GLL format is: 
S = {p, q, {r, s, t, {}, {u, v}, w, x, {y, z}, a, b}, A, B}

(Note: Two-character labels 'a1', 'b1' were mapped to single characters 'A', 'B', 'a', 'b' due to node structure limitations.)

Destroying GLL and freeing memory_npk...
Cleanup complete_npk.
PS C:\Users\Nandini\Documents\DS_VIT>

```