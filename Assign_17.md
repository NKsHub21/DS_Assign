
# ASSIGNMENT NO - 7 Unit_2
<p align="center">Polynomial Addition using Singly Linked List</p>

---

## Polynomial Representation

A polynomial is an expression consisting of variables (indeterminates) and coefficients, involving only the operations of addition, subtraction, multiplication, and non-negative integer exponents.

In this program, a **Singly Linked List** is used to represent a polynomial. Each node in the list stores one term of the polynomial:

1.  **Coefficient Field** (`coeff_npk`): The numerical multiplier of the term.
2.  **Exponent Field** (`exp_npk`): The power of the variable (e.g., $x^2$).
3.  **Pointer Field** (`next_npk`): Points to the next term in the polynomial.

The polynomial terms are typically stored in descending order of their exponents for simplified processing.

---

##  Algorithm: Polynomial Addition

The addition process involves traversing both polynomial lists simultaneously and creating a new resultant list.

### 1. Addition Logic

```

1.  Start.
2.  Initialize three pointers: p1\_npk (for Poly 1), p2\_npk (for Poly 2), and result\_npk (for the Resultant Poly).
3.  While both p1\_npk and p2\_npk are not NULL:
    a. If p1\_npk-\>exp\_npk == p2\_npk-\>exp\_npk:
    i. Add coefficients: sum = p1\_npk-\>coeff\_npk + p2\_npk-\>coeff\_npk.
    ii. Create a new node in the result list with (sum, p1\_npk-\>exp\_npk).
    iii. Advance both p1\_npk and p2\_npk.
    b. If p1\_npk-\>exp\_npk \> p2\_npk-\>exp\_npk:
    i. The term from Poly 1 is unique.
    ii. Copy (p1\_npk-\>coeff\_npk, p1\_npk-\>exp\_npk) to the result list.
    iii. Advance p1\_npk.
    c. If p2\_npk-\>exp\_npk \> p1\_npk-\>exp\_npk:
    i. The term from Poly 2 is unique.
    ii. Copy (p2\_npk-\>coeff\_npk, p2\_npk-\>exp\_npk) to the result list.
    iii. Advance p2\_npk.
4.  After the main loop, one list might have remaining terms. Copy all remaining nodes from the non-NULL list to the result list.
5.  Return the result list head.
6.  End.

<!-- end list -->

````

---

## C++ Code Implementation

```cpp
#include <iostream>
#include <cstdlib> // For malloc/free

using namespace std;

// Structure Definition
typedef struct polynomial_npk {
    int coeff_npk; 
    int exp_npk;
    struct polynomial_npk* next_npk;
} PolyNode_npk;

// Global Function Prototypes
PolyNode_npk* getNode_npk(void);
PolyNode_npk* createPolynomial_npk(void);
void printPolynomial_npk(PolyNode_npk* head_npk);
PolyNode_npk* addPolynomials_npk(PolyNode_npk* poly1_npk, PolyNode_npk* poly2_npk);
void insertTerm_npk(PolyNode_npk** head_ref_npk, int coeff_npk, int exp_npk);

// Node Allocator (Using malloc as requested)
PolyNode_npk* getNode_npk() {
    PolyNode_npk* newNode_npk = (PolyNode_npk*)malloc(sizeof(PolyNode_npk));
    if (!newNode_npk) {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    newNode_npk->coeff_npk = 0;
    newNode_npk->exp_npk = 0;
    newNode_npk->next_npk = NULL;
    return newNode_npk;
}

// Function to insert a new term into the polynomial (used by create and add)
void insertTerm_npk(PolyNode_npk** head_ref_npk, int coeff_npk, int exp_npk) {
    if (coeff_npk == 0) return; // Do not insert zero terms

    PolyNode_npk* newNode_npk = getNode_npk();
    newNode_npk->coeff_npk = coeff_npk;
    newNode_npk->exp_npk = exp_npk;
    
    // Simple insertion at the end (assuming user enters in descending order, 
    // or relying on addPolynomials to handle ordering)
    if (*head_ref_npk == NULL) {
        *head_ref_npk = newNode_npk;
    } else {
        PolyNode_npk* temp_npk = *head_ref_npk;
        while (temp_npk->next_npk != NULL) {
            temp_npk = temp_npk->next_npk;
        }
        temp_npk->next_npk = newNode_npk;
    }
}

// Create Initial Polynomial List
PolyNode_npk* createPolynomial_npk() {
    PolyNode_npk* head_npk = NULL;
    int coeff_npk, exp_npk, choice_npk;

    cout << "\n--- Creating New Polynomial ---\n";
    while (1) {
        cout << "Enter term [1-Yes | 0-No]: ";
        cin >> choice_npk;
        if (choice_npk == 0)
            break;

        cout << "Enter Coefficient: ";
        cin >> coeff_npk;
        cout << "Enter Exponent: ";
        cin >> exp_npk;

        insertTerm_npk(&head_npk, coeff_npk, exp_npk);
    }
    return head_npk;
}

// Print Polynomial List
void printPolynomial_npk(PolyNode_npk* head_npk) {
    if (head_npk == NULL) {
        cout << "0\n";
        return;
    }
    PolyNode_npk* current_npk = head_npk;
    while (current_npk != NULL) {
        if (current_npk != head_npk && current_npk->coeff_npk > 0) {
            cout << " + ";
        } else if (current_npk->coeff_npk < 0) {
            // If negative, print sign as part of coefficient
            if (current_npk != head_npk) cout << " ";
        }

        if (current_npk->exp_npk == 0) {
            cout << current_npk->coeff_npk;
        } else if (current_npk->exp_npk == 1) {
            cout << current_npk->coeff_npk << "x";
        } else {
            cout << current_npk->coeff_npk << "x^" << current_npk->exp_npk;
        }

        current_npk = current_npk->next_npk;
    }
    cout << "\n";
}

// Add two Polynomials
PolyNode_npk* addPolynomials_npk(PolyNode_npk* poly1_npk, PolyNode_npk* poly2_npk) {
    PolyNode_npk* p1_npk = poly1_npk;
    PolyNode_npk* p2_npk = poly2_npk;
    PolyNode_npk* result_head_npk = NULL;

    while (p1_npk != NULL || p2_npk != NULL) {
        int sum_coeff_npk;
        int max_exp_npk;

        if (p1_npk == NULL) {
            // Poly 1 is finished, copy remaining of Poly 2
            sum_coeff_npk = p2_npk->coeff_npk;
            max_exp_npk = p2_npk->exp_npk;
            p2_npk = p2_npk->next_npk;
        } else if (p2_npk == NULL) {
            // Poly 2 is finished, copy remaining of Poly 1
            sum_coeff_npk = p1_npk->coeff_npk;
            max_exp_npk = p1_npk->exp_npk;
            p1_npk = p1_npk->next_npk;
        } else if (p1_npk->exp_npk == p2_npk->exp_npk) {
            // Exponents match: add coefficients
            sum_coeff_npk = p1_npk->coeff_npk + p2_npk->coeff_npk;
            max_exp_npk = p1_npk->exp_npk;
            p1_npk = p1_npk->next_npk;
            p2_npk = p2_npk->next_npk;
        } else if (p1_npk->exp_npk > p2_npk->exp_npk) {
            // Term from Poly 1 is larger
            sum_coeff_npk = p1_npk->coeff_npk;
            max_exp_npk = p1_npk->exp_npk;
            p1_npk = p1_npk->next_npk;
        } else { // p2_npk->exp_npk > p1_npk->exp_npk
            // Term from Poly 2 is larger
            sum_coeff_npk = p2_npk->coeff_npk;
            max_exp_npk = p2_npk->exp_npk;
            p2_npk = p2_npk->next_npk;
        }

        if (sum_coeff_npk != 0) {
            insertTerm_npk(&result_head_npk, sum_coeff_npk, max_exp_npk);
        }
    }

    return result_head_npk;
}


int main() {
    PolyNode_npk* poly1_npk = NULL;
    PolyNode_npk* poly2_npk = NULL;
    PolyNode_npk* result_npk = NULL;

    // Create Polynomial 1
    poly1_npk = createPolynomial_npk();
    cout << "\nPolynomial 1: ";
    printPolynomial_npk(poly1_npk);

    // Create Polynomial 2
    poly2_npk = createPolynomial_npk();
    cout << "Polynomial 2: ";
    printPolynomial_npk(poly2_npk);

    // Add Polynomials
    result_npk = addPolynomials_npk(poly1_npk, poly2_npk);

    // Display Result
    cout << "\n=========================================\n";
    cout << "Sum of Polynomials: ";
    printPolynomial_npk(result_npk);
    cout << "=========================================\n";
    
    // Clean up memory (optional, but good practice)
    // In a real implementation, destroy functions would be needed for poly1 and poly2 too.
    // For this simple WAP, we just free the result.
    // NOTE: For brevity, destroy functions for poly1 and poly2 are omitted.
    
    PolyNode_npk* current_npk;
    while(result_npk != NULL) {
        current_npk = result_npk;
        result_npk = result_npk->next_npk;
        free(current_npk);
    }


    return 0;
}
````

```
```

## Output

PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_17.cpp -o Assign_17 } ; if ($?) { .\Assign_17 }

--- Creating New Polynomial (Enter terms in descending exponent order) ---
Enter term [1-Yes | 0-No]: 1
Enter Coefficient: 23
Enter Exponent: 2
Enter term [1-Yes | 0-No]: 0

Polynomial 1: 23x^2

--- Creating New Polynomial (Enter terms in descending exponent order) ---
Enter term [1-Yes | 0-No]: