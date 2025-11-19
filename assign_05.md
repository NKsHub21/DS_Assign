# <center> ASSIGNMENT NO - 5 Unit_1 </center>

## Title : Develop a program to compute the fast transpose of a sparse matrix using its compact (triplet) representation efficiently

## Sparse Matrix - Compact (Triplet) Representation & Fast Transpose Algorithm

#### **Compact (Triplet) Representation**  
Instead of storing all elements, a sparse matrix can be stored as a list of non-zero elements. Each element is stored as a triplet (row, column, value). The first row often contains metadata: [number of rows, number of columns, number of non-zero elements].

Structure -

    Row | Column| Value
    0	| 2     |	3
    2	| 0	    |   4


#### **Fast Transpose Algorithm**  
The fast transpose algorithm efficiently computes the transpose in O(num_nonzero + n) time, where num_nonzero is the number of non-zero elements and n is the number of columns.

Steps:  
    1.Count the number of elements in each column of the original matrix.  
    2.Compute the starting position of each column in the transposed matrix.  
    3.Place each element directly at its correct position in the transposed matrix using the starting positions.

---
## Algorithm
```
1. Start
2. Input m (rows), n (cols), t (non-zero terms)
3. Input sparse matrix a[0 to t] where:
    - a[0] = {m, n, t}
    - a[1 to t] = {row, col, val}
4. Initialize b[0 to t]
    - b[0] = {n, m, t}
5. Initialize row_terms[n] = 0
6. For i = 1 to t
    row_terms[a[i][1]]++ 
7. Compute start_pos[0 to n - 1]:
    start_pos[0] = 1
    For i = 1 to n - 1
        start_pos[i] = start_pos[i - 1] + row_terms[i - 1]
8. For i = 1 to t
    j = start_pos[a[i][1]]++
    b[j][0] = a[i][1]
    b[j][1] = a[i][0]
    b[j][2] = a[i][2]
9. Print original sparse matrix and fast transposed sparse matrix
10. End
```

---
# Code
```c
#include <iostream>
#include <cstdlib>
using namespace std;

void fastTranspose_npk(int **original_npk, int **transposed_npk) {
    int rows_npk, cols_npk, nonZero_npk, i_npk, j_npk;

    rows_npk = original_npk[0][0];
    cols_npk = original_npk[0][1];
    nonZero_npk = original_npk[0][2];

    transposed_npk[0][0] = cols_npk;
    transposed_npk[0][1] = rows_npk;
    transposed_npk[0][2] = nonZero_npk;

    if (nonZero_npk > 0) {
        int *rowTerms_npk = (int *)malloc(cols_npk * sizeof(int));
        int *startPos_npk = (int *)malloc(cols_npk * sizeof(int));

        for (i_npk = 0; i_npk < cols_npk; i_npk++)
            rowTerms_npk[i_npk] = 0;

        // Count number of entries in each column
        for (i_npk = 1; i_npk <= nonZero_npk; i_npk++)
            rowTerms_npk[original_npk[i_npk][1]]++;

        // Starting position for each row in transposed matrix
        startPos_npk[0] = 1;
        for (i_npk = 1; i_npk < cols_npk; i_npk++)
            startPos_npk[i_npk] = startPos_npk[i_npk - 1] + rowTerms_npk[i_npk - 1];

        // Fill transposed matrix
        for (i_npk = 1; i_npk <= nonZero_npk; i_npk++) {
            j_npk = startPos_npk[original_npk[i_npk][1]]++;
            transposed_npk[j_npk][0] = original_npk[i_npk][1];
            transposed_npk[j_npk][1] = original_npk[i_npk][0];
            transposed_npk[j_npk][2] = original_npk[i_npk][2];
        }

        free(rowTerms_npk);
        free(startPos_npk);
    }
}

int main() {
    int rows_npk, cols_npk, nonZero_npk, i_npk;

    cout << "Enter number of rows and columns: ";
    cin >> rows_npk >> cols_npk;

    cout << "Enter number of non-zero elements: ";
    cin >> nonZero_npk;

    int **original_npk = (int **)malloc((nonZero_npk + 1) * sizeof(int *));
    int **transposed_npk = (int **)malloc((nonZero_npk + 1) * sizeof(int *));

    for (i_npk = 0; i_npk <= nonZero_npk; i_npk++) {
        original_npk[i_npk] = (int *)malloc(3 * sizeof(int));
        transposed_npk[i_npk] = (int *)malloc(3 * sizeof(int));
    }

    // Store header info
    original_npk[0][0] = rows_npk;
    original_npk[0][1] = cols_npk;
    original_npk[0][2] = nonZero_npk;

    cout << "Enter row, column, value for each non-zero element:" << endl;
    for (i_npk = 1; i_npk <= nonZero_npk; i_npk++) {
        cin >> original_npk[i_npk][0] >> original_npk[i_npk][1] >> original_npk[i_npk][2];
    }

    fastTranspose_npk(original_npk, transposed_npk);

    cout << "\nOriginal Sparse Matrix (Triplet Form):" << endl;
    for (i_npk = 0; i_npk <= nonZero_npk; i_npk++) {
        cout << original_npk[i_npk][0] << "\t" 
             << original_npk[i_npk][1] << "\t" 
             << original_npk[i_npk][2] << endl;
    }

    cout << "\nFast Transpose (Triplet Form):" << endl;
    for (i_npk = 0; i_npk <= nonZero_npk; i_npk++) {
        cout << transposed_npk[i_npk][0] << "\t" 
             << transposed_npk[i_npk][1] << "\t" 
             << transposed_npk[i_npk][2] << endl;
    }

    for (i_npk = 0; i_npk <= nonZero_npk; i_npk++) {
        free(original_npk[i_npk]);
        free(transposed_npk[i_npk]);
    }
    free(original_npk);
    free(transposed_npk);

    return 0;
}

```

---
# Output
```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ FastTranspose.cpp -o FastTranspose } ; if ($?) { .\FastTranspose }
Enter number of rows and columns: 3 3
Enter number of non-zero elements: 4
Enter row, col, value for each non-zero element:
0 0 1
0 2 2
1 1 3
2 0 4

Original Sparse Matrix (Triplet form):
3       3       4
0       0       1
0       2       2
1       1       3
2       0       4

Fast Transpose Result (Triplet form):
3       3       4
0       0       1
0       2       4
1       1       3
2       0       2