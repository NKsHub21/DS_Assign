# ASSIGNMENT NO - 4 Unit_2
<p align="center">Set Operations (Cricket & Football) using Singly Linked Lists</p>

---

## Concept: Set Representation via Linked Lists

In this program, we use **Singly Linked Lists** to represent the three primary sets of students:

1.  **Universal Set (U):** The total population of students in the Second Year Computer Engineering class (includes all students regardless of preference). This must be defined and created first.
2.  **Set A:** Students who like Cricket.
3.  **Set B:** Students who like Football.

Each node in the list stores a student's **Roll Number** (`roll_npk`) and **Name** (`name_npk`). Since set operations rely on unique identification, the Roll Number is critical for comparison.

## Algorithms: Set Operations

Set operations are performed by traversing the lists and comparing the `roll_npk` values.

### a) Intersection (Set A $\cap$ Set B): Likes Both

Finds students present in **both** Set A (Cricket) and Set B (Football).

Start with Set A and Set B heads.

Initialize Result List (Intersection_npk).

Traverse every node in Set A (tempA_npk).

For each tempA_npk, traverse Set B (tempB_npk) to search for a matching roll_npk.

If a match is found:
a. Create a new node and copy the student data to Intersection_npk.
b. Break the inner traversal and move to the next node in Set A.

Return Intersection_npk head.

End.


### b) Symmetric Difference (Set A $\oplus$ Set B): Likes Either, But Not Both

Finds students present in **Set A OR Set B**, but **not** in the Intersection.

Start with Set A and Set B heads.

Initialize Result List (SymmetricDiff_npk).

Traverse Set A: If a student from Set A is NOT found in Set B, copy them to SymmetricDiff_npk.

Traverse Set B: If a student from Set B is NOT found in Set A, copy them to SymmetricDiff_npk.

(Note: A separate helper function is needed to check if a roll_npk exists in another set.)

Return SymmetricDiff_npk head.

End.


### c) Neither (U - (Set A $\cup$ Set B)): Neither Cricket Nor Football

Finds students in the Universal Set (U) who are **not** present in either Set A or Set B. This requires finding the Union first.

Find Union (Set A U Set B): Create a list containing all unique students from A and B.

Initialize Result Count = 0.

Traverse the Universal Set (U).

For each student in U, check if their roll_npk exists in the Union list.

If the student is NOT found in the Union list:
a. Increment Result Count.

Display Result Count.

End.


---

## C++ Code Implementation

```cpp
#include <iostream>
#include <cstdlib>
#include <cstring>

using namespace std;

// Structure Definition
typedef struct student_set_npk {
    int roll_npk; 
    char name_npk[50];
    struct student_set_npk* next_npk;
} Node_npk;

// Function Prototypes
Node_npk* getNode_npk(void);
Node_npk* createSet_npk(const char* setName_npk);
void printSet_npk(Node_npk* head_npk, const char* setName_npk);
bool isMember_npk(Node_npk* head_npk, int roll_npk);
void insertEnd_npk(Node_npk** head_ref_npk, int roll_npk, const char* name_npk);
Node_npk* intersection_npk(Node_npk* setA_npk, Node_npk* setB_npk);
Node_npk* symmetricDifference_npk(Node_npk* setA_npk, Node_npk* setB_npk);
Node_npk* union_npk(Node_npk* setA_npk, Node_npk* setB_npk);
int countNeither_npk(Node_npk* universal_npk, Node_npk* union_npk);
void destroyList_npk(Node_npk* head_npk);

// --- Core Helper Functions ---

// Node Allocator (Using malloc as requested)
Node_npk* getNode_npk() {
    Node_npk* newNode_npk = (Node_npk*)malloc(sizeof(Node_npk));
    if (!newNode_npk) {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    newNode_npk->roll_npk = 0;
    newNode_npk->next_npk = NULL;
    return newNode_npk;
}

// Function to check if a roll_npk exists in a set
bool isMember_npk(Node_npk* head_npk, int roll_npk) {
    Node_npk* current_npk = head_npk;
    while (current_npk != NULL) {
        if (current_npk->roll_npk == roll_npk) {
            return true;
        }
        current_npk = current_npk->next_npk;
    }
    return false;
}

// Helper to insert a node at the end
void insertEnd_npk(Node_npk** head_ref_npk, int roll_npk, const char* name_npk) {
    Node_npk* newNode_npk = getNode_npk();
    newNode_npk->roll_npk = roll_npk;
    // Use strncpy for safety
    strncpy(newNode_npk->name_npk, name_npk, 49);
    newNode_npk->name_npk[49] = '\0';

    if (*head_ref_npk == NULL) {
        *head_ref_npk = newNode_npk;
        return;
    }

    Node_npk* temp_npk = *head_ref_npk;
    while (temp_npk->next_npk != NULL) {
        temp_npk = temp_npk->next_npk;
    }
    temp_npk->next_npk = newNode_npk;
}

// Create Initial Set (Universal, A, or B)
Node_npk* createSet_npk(const char* setName_npk) {
    Node_npk* head_npk = NULL;
    int roll_npk, choice_npk;
    char name_npk[50];

    cout << "\n--- Creating Set " << setName_npk << " ---\n";
    while (1) {
        cout << "Add student to " << setName_npk << " [1-Yes | 0-No]: ";
        if (!(cin >> choice_npk)) {
            cout << "Invalid input. Exiting set creation.\n";
            cin.clear();
            cin.ignore(10000, '\n');
            break;
        }
        
        if (choice_npk == 0)
            break;

        cout << "Enter Roll No (Unique): ";
        if (!(cin >> roll_npk)) {
            cout << "Invalid Roll No. Skipping.\n";
            cin.clear();
            cin.ignore(10000, '\n');
            continue;
        }
        cout << "Enter Name (No Spaces): ";
        cin >> name_npk; // Reads up to the first whitespace

        // Check for duplicates before inserting (Crucial for sets)
        if (isMember_npk(head_npk, roll_npk)) {
            cout << "Roll No " << roll_npk << " already exists in this set. Skipping.\n";
            continue;
        }

        insertEnd_npk(&head_npk, roll_npk, name_npk);
    }
    return head_npk;
}

// Print Set
void printSet_npk(Node_npk* head_npk, const char* setName_npk) {
    cout << "Set " << setName_npk << ": {";
    if (head_npk == NULL) {
        cout << "}\n";
        return;
    }
    
    Node_npk* current_npk = head_npk;
    while (current_npk != NULL) {
        cout << current_npk->name_npk << " (" << current_npk->roll_npk << ")";
        if (current_npk->next_npk != NULL) {
            cout << ", ";
        }
        current_npk = current_npk->next_npk;
    }
    cout << "}\n";
}

// Function to destroy a list and free memory
void destroyList_npk(Node_npk* head_npk) {
    Node_npk* temp_npk;
    while (head_npk != NULL) {
        temp_npk = head_npk;
        head_npk = head_npk->next_npk;
        free(temp_npk);
    }
}


// --- Set Operation Implementations ---

// a) Intersection (A ∩ B): Likes both Cricket and Football
Node_npk* intersection_npk(Node_npk* setA_npk, Node_npk* setB_npk) {
    Node_npk* result_npk = NULL;
    Node_npk* tempA_npk = setA_npk;

    while (tempA_npk != NULL) {
        if (isMember_npk(setB_npk, tempA_npk->roll_npk)) {
            insertEnd_npk(&result_npk, tempA_npk->roll_npk, tempA_npk->name_npk);
        }
        tempA_npk = tempA_npk->next_npk;
    }
    return result_npk;
}

// Helper: Union (A ∪ B) - Required for part c
Node_npk* union_npk(Node_npk* setA_npk, Node_npk* setB_npk) {
    Node_npk* result_npk = NULL;
    Node_npk* current_npk;

    // 1. Copy all elements of Set A
    current_npk = setA_npk;
    while (current_npk != NULL) {
        insertEnd_npk(&result_npk, current_npk->roll_npk, current_npk->name_npk);
        current_npk = current_npk->next_npk;
    }

    // 2. Copy elements of Set B that are NOT yet in the result list
    current_npk = setB_npk;
    while (current_npk != NULL) {
        // Check membership against the result list (which contains A)
        if (!isMember_npk(result_npk, current_npk->roll_npk)) {
            insertEnd_npk(&result_npk, current_npk->roll_npk, current_npk->name_npk);
        }
        current_npk = current_npk->next_npk;
    }

    return result_npk;
}


// b) Symmetric Difference (A XOR B): Likes either, but not both
Node_npk* symmetricDifference_npk(Node_npk* setA_npk, Node_npk* setB_npk) {
    Node_npk* result_npk = NULL;
    Node_npk* current_npk;

    // 1. Check for members in A but NOT in B (A - B)
    current_npk = setA_npk;
    while (current_npk != NULL) {
        if (!isMember_npk(setB_npk, current_npk->roll_npk)) {
            insertEnd_npk(&result_npk, current_npk->roll_npk, current_npk->name_npk);
        }
        current_npk = current_npk->next_npk;
    }

    // 2. Check for members in B but NOT in A (B - A)
    current_npk = setB_npk;
    while (current_npk != NULL) {
        if (!isMember_npk(setA_npk, current_npk->roll_npk)) {
            insertEnd_npk(&result_npk, current_npk->roll_npk, current_npk->name_npk);
        }
        current_npk = current_npk->next_npk;
    }
    return result_npk;
}

// c) Count Neither (U - (A ∪ B)): Neither Cricket nor Football
int countNeither_npk(Node_npk* universal_npk, Node_npk* union_npk) {
    int count_npk = 0;
    Node_npk* current_npk = universal_npk;

    while (current_npk != NULL) {
        // If student from Universal Set is NOT found in the Union (A U B), 
        // they like NEITHER.
        if (!isMember_npk(union_npk, current_npk->roll_npk)) {
            count_npk++;
        }
        current_npk = current_npk->next_npk;
    }
    return count_npk;
}


// --- Main Execution ---

int main() {
    // 1. Define the Universal Set (Total Class Strength)
    Node_npk* universal_npk = createSet_npk("U (Universal Set: All Students)");

    // 2. Define Set A (Cricket) and Set B (Football)
    Node_npk* setA_npk = createSet_npk("A (Cricket)");
    Node_npk* setB_npk = createSet_npk("B (Football)");

    cout << "\n=========================================\n";
    cout << "              SET ANALYSIS\n";
    cout << "=========================================\n";
    
    printSet_npk(universal_npk, "U (Total Students)");
    printSet_npk(setA_npk, "A (Cricket)");
    printSet_npk(setB_npk, "B (Football)");
    cout << "-----------------------------------------\n";

    // a) Intersection (A ∩ B)
    Node_npk* intersectionResult_npk = intersection_npk(setA_npk, setB_npk);
    cout << "a) Likes Both (A ∩ B):\n";
    printSet_npk(intersectionResult_npk, "Intersection");
    cout << "-----------------------------------------\n";

    // b) Symmetric Difference (A XOR B)
    Node_npk* symmetricDiffResult_npk = symmetricDifference_npk(setA_npk, setB_npk);
    cout << "b) Likes Either, But Not Both (A XOR B):\n";
    printSet_npk(symmetricDiffResult_npk, "Symmetric Difference");
    cout << "-----------------------------------------\n";

    // c) Neither (U - (A U B))
    Node_npk* unionResult_npk = union_npk(setA_npk, setB_npk);
    int neitherCount_npk = countNeither_npk(universal_npk, unionResult_npk);
    
    cout << "c) Number of students who like NEITHER:\n";
    cout << "Total students who like neither Cricket nor Football: " << neitherCount_npk << "\n";
    cout << "=========================================\n";

    // Clean up memory
    destroyList_npk(universal_npk);
    destroyList_npk(setA_npk);
    destroyList_npk(setB_npk);
    destroyList_npk(intersectionResult_npk);
    destroyList_npk(symmetricDiffResult_npk);
    destroyList_npk(unionResult_npk); 

    return 0;
}

## Output
```

PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_14.cpp -o Assign_14 } ; if ($?) { .\Assign_14 }

--- Creating Set U (Universal Set: All Students) ---
Add student to U (Universal Set: All Students) [1-Yes | 0-No]: 1
Enter Roll No (Unique): 23
Enter Name (No Spaces): Uday
Add student to U (Universal Set: All Students) [1-Yes | 0-No]: 1
Enter Roll No (Unique): 34
Enter Name (No Spaces): Krish
Add student to U (Universal Set: All Students) [1-Yes | 0-No]: 0

--- Creating Set A (Cricket) ---
Add student to A (Cricket) [1-Yes | 0-No]: 1
Enter Roll No (Unique): 23
Enter Name (No Spaces): Uday
Add student to A (Cricket) [1-Yes | 0-No]: 0

--- Creating Set B (Football) ---
Add student to B (Football) [1-Yes | 0-No]: 1
Enter Roll No (Unique): 34
Enter Name (No Spaces): Krish
Add student to B (Football) [1-Yes | 0-No]: 0

=========================================
              SET ANALYSIS
=========================================
Set U (Total Students): {Uday (23), Krish (34)}
Set A (Cricket): {Uday (23)}
Set B (Football): {Krish (34)}
-----------------------------------------
a) Likes Both (A Γê⌐ B):
Set Intersection: {}
-----------------------------------------
b) Likes Either, But Not Both (A XOR B):
Set Symmetric Difference: {Uday (23), Krish (34)}
-----------------------------------------
c) Number of students who like NEITHER:
Total students who like neither Cricket nor Football: 0
=========================================
PS C:\Users\Nandini\Documents\DS_VIT>

```