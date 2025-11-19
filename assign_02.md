# ASSIGNMENT NO - 2 UNIT_1

## Title :
Write a program to construct and verify a magic square of order 'n' (for both even & odd) such that all rows, columns, and diagonals sum to the same value.

---

## What is a Magic Square?  

A **Magic Square** is an `n × n` matrix filled with numbers from `1` to `n²` such that the **sum of each row, each column, and both diagonals is the same**.  
This constant value is called the **magic sum** and is given by:  

\[
Magic\ Sum = \frac{n (n^2 + 1)}{2}
\]

Example: A 3×3 magic square looks like this:

```

8  1  6
3  5  7
4  9  2

````

Here, every row, column, and diagonal adds up to 15.

---

## Algorithm (Step-by-Step) (Odd n only)

**Goal:** Fill an `n × n` matrix (where `n` is odd) with numbers `1 .. n²` so that every row, column, and both diagonals sum to the same magic sum.

**Method (Siamese / De la Loubère):**

1. Read `n`.  
   If `n <= 0` or `n` is even → stop with error (works only for odd n).  
2. Dynamically allocate an `n × n` matrix and initialize every cell to 0.  
3. Set `row = 0` and `col = n / 2` (top row, middle column).  
4. For `num` from 1 to `n * n`:
   - Place `num` at `matrix[row][col]`.  
   - Compute tentative next position:  
     `next_row = row - 1` (move up)  
     `next_col = col + 1` (move right)  
   - Wrap around edges:  
     if `next_row < 0` → `next_row = n - 1`  
     if `next_col == n` → `next_col = 0`  
   - If `matrix[next_row][next_col] != 0` (already occupied),  
     then move down one step from current cell:  
     `next_row = (row + 1) % n`  
     `next_col = col`  
   - Update `row = next_row; col = next_col`.  
5. Print the matrix and the magic sum.  
6. Free all dynamically allocated memory.

---
```
## Code

```cpp
#include <iostream>
#include <cstdlib>
#include <iomanip>

using namespace std;

int main() {
    int n_npk;

    cout << "Enter the size of the magic square (odd number): ";
    cin >> n_npk;

    if (n_npk <= 0 || n_npk % 2 == 0) {
        cout << "Error: Please enter a positive odd number." << endl;
        return -1;
    }

    int** magicsqr_npk = (int**)malloc(n_npk * sizeof(int*));
    if (magicsqr_npk == NULL) {
        cout << "Memory allocation failed." << endl;
        return -1;
    }

    for (int i = 0; i < n_npk; i++) {
        magicsqr_npk[i] = (int*)malloc(n_npk * sizeof(int));
        if (magicsqr_npk[i] == NULL) {
            cout << "Memory allocation failed." << endl;
            return -2;
        }
        for (int j = 0; j < n_npk; j++) {
            magicsqr_npk[i][j] = 0;
        }
    }

    int row_npk = 0;
    int col_npk = n_npk / 2;

    for (int num_npk = 1; num_npk <= n_npk * n_npk; num_npk++) {
        magicsqr_npk[row_npk][col_npk] = num_npk;

        int next_row_npk = row_npk - 1;
        int next_col_npk = col_npk + 1;

        if (next_row_npk < 0) next_row_npk = n_npk - 1;
        if (next_col_npk == n_npk) next_col_npk = 0;

        if (magicsqr_npk[next_row_npk][next_col_npk] != 0) {
            next_row_npk = (row_npk + 1) % n_npk;
            next_col_npk = col_npk;
        }

        row_npk = next_row_npk;
        col_npk = next_col_npk;
    }

    cout << "\n=== Magic Square (" << n_npk << "x" << n_npk << ") ===\n";
    for (int i = 0; i < n_npk; i++) {
        for (int j = 0; j < n_npk; j++) {
            cout << setw(4) << magicsqr_npk[i][j];
        }
        cout << endl;
    }

    int magic_sum = n_npk * (n_npk * n_npk + 1) / 2;
    cout << "\nMagic constant (sum of each row/col/diag): " 
         << magic_sum << endl;

    for (int i = 0; i < n_npk; i++) {
        free(magicsqr_npk[i]);
    }
    free(magicsqr_npk);

    return 0;
}
````

---

## Output

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
Enter the size of the magic square (odd number): 3

=== Magic Square (3x3) ===
   8   1   6
   3   5   7
   4   9   2

Magic constant (sum of each row/col/diag): 15
```



