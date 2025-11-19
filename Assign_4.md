# <center> ASSIGNMENT NO - 4 Unit_1</center>

## Title : Develop a program to identify and efficiently store a sparse matrix using compact representation and perform basic operations like display and simple transpose

# Sparse Matrix

## What is a Sparse Matrix?

A **sparse matrix** is a matrix in which most of the elements are zero.

**Definition:**  
A matrix is considered *sparse* when the number of zero elements is significantly more than the number of non-zero elements.

👉 In the sparse matrix concept, we try to **reduce the memory usage** by storing only the non-zero elements and their positions.

---

## Algorithm (Based on the Given Pseudocode)

**Algorithm: Sparse Matrix Representation**

1. Start  
2. Read the number of rows `m` and columns `n`.  
3. Declare a 2D array of size `m × n` using dynamic memory (float **matrix).  
4. Initialize `counter = 0`.  
5. For each element in the matrix:  
   - Read element.  
   - If element ≠ 0, increment `counter`.  
6. Allocate memory for the sparse matrix of size `(counter + 1)`.  
   - `sparse[0]` will store `{row = m, col = n, val = counter}`.  
7. Initialize `k = 1`.  
8. For each element in the matrix:  
   - If `matrix[i][j] ≠ 0`:  
     - Store `i, j, matrix[i][j]` into `sparse[k]`.  
     - Increment `k`.  
9. Print the sparse matrix in **Row, Col, Value** format.  
10. Free all dynamically allocated memory.  
11. End.  

---

## code

#include <iostream>
#include <cstdlib> 

using namespace std;

typedef struct Sparse_npk
{
    int row_npk, col_npk;
    float val_npk;
} SPR_npk;

int main(void)
{
    int m_npk, n_npk;
    float** matrix_npk = NULL;
    SPR_npk* sparse_npk = NULL;
    int i, j;

    cout << "Enter number of rows: ";
    cin >> m_npk;

    cout << "Enter number of columns: ";
    cin >> n_npk;

    matrix_npk = (float**)malloc(m_npk * sizeof(float*));
    if (matrix_npk == NULL)
    {
        cout << "Memory allocation failed." << endl;
        exit(-1);
    }

    for (i = 0; i < m_npk; i++)
    {
        matrix_npk[i] = (float*)malloc(n_npk * sizeof(float));
        if (matrix_npk[i] == NULL)
        {
            cout << "Memory allocation failed." << endl;
            exit(-2);
        }
    }

    int counter_npk = 0;

    cout << "\nEnter elements row by row (" << m_npk * n_npk << " values):\n";
    for (i = 0; i < m_npk; i++)
    {
        for (j = 0; j < n_npk; j++)
        {
            cin >> matrix_npk[i][j];
            if (matrix_npk[i][j] != 0.0f)
                counter_npk++;
        }
    }

    cout << "\n=== Original Matrix (" << m_npk << "x" << n_npk << ") ===\n";
    for (i = 0; i < m_npk; i++)
    {
        for (j = 0; j < n_npk; j++)
        {
            cout << matrix_npk[i][j] << "\t";
        }
        cout << endl;
    }

    sparse_npk = (SPR_npk*)malloc((counter_npk + 1) * sizeof(SPR_npk));

    sparse_npk[0].row_npk = m_npk;
    sparse_npk[0].col_npk = n_npk;
    sparse_npk[0].val_npk = (float)counter_npk;

    int k = 1;
    for (i = 0; i < m_npk; i++)
    {
        for (j = 0; j < n_npk; j++)
        {
            if (matrix_npk[i][j] != 0.0f)
            {
                sparse_npk[k].row_npk = i;
                sparse_npk[k].col_npk = j;
                sparse_npk[k].val_npk = matrix_npk[i][j];
                k++;
            }
        }
    }

    cout << "\n=== Sparse Matrix (Triplet Form) ===\n";
    cout << "Row\tCol\tValue\n";
    cout << "-------------------------\n";
    for (i = 0; i <= counter_npk; i++)
    {
        cout << sparse_npk[i].row_npk << "\t"
             << sparse_npk[i].col_npk << "\t"
             << sparse_npk[i].val_npk << endl;
    }

    cout << "\n=== Transpose of Original Matrix ===\n";
    for (j = 0; j < n_npk; j++)
    {
        for (i = 0; i < m_npk; i++)
        {
            cout << matrix_npk[i][j] << "\t";
        }
        cout << endl;
    }

    for (i = 0; i < m_npk; i++)
    {
        free(matrix_npk[i]);
    }
    free(matrix_npk);
    free(sparse_npk);

    return 0;
}

## Output

PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Sparse_matrix.cpp -o Sparse_matrix } ; if ($?) { .\Sparse_matrix }
Enter number of rows: 3
Enter number of columns: 3

Enter elements row by row (9 values):
 1 2 3 4 5 6 7 8 9

=== Original Matrix (3x3) ===
1       2       3
4       5       6
7       8       9

=== Sparse Matrix (Triplet Form) ===
Row     Col     Value
-------------------------
3       3       9
0       0       1
0       1       2
0       2       3
1       0       4
1       1       5
1       2       6
2       0       7
2       1       8
2       2       9

=== Transpose of Original Matrix ===
1       4       7
2       5       8
3       6       9

