# <center> ASSIGNMENT NO -3 Unit_1 </center>

## Title : Implement matrix multiplication and analyse its performance using row-major vs column-major order access patterns to understand how memory layout affects cache performance

## What is Row-major and Column-major ?
row-major order and column-major order are methods for **storing multidimensional arrays in linear storage** such as random access memory.  
Row-major order stores elements row by row, with elements of the same row placed contiguously in memory.   
Column-major order stores elements column by column, with elements of the same column placed contiguously.
 


## Algorithm


1. Read integers m, n, p
2. Declare A[n][m], B[p][n], C[p][m]   // Note: Stored column-wise (columns of rows)

3. For j = 0 to n-1:       // For each column of A
       For i = 0 to m-1:
           Read A[j][i]    // Store A in column-major (A[j][i] instead of A[i][j])

4. For j = 0 to p-1:       // For each column of B
       For i = 0 to n-1:
           Read B[j][i]    // Store B in column-major

5. For j = 0 to p-1:
       For i = 0 to m-1:
           Set C[j][i] = 0    // Initialize result matrix column-wise

6. For j = 0 to p-1:           // Each column of C (and B)
       For i = 0 to m-1:       // Each row of C (and A)
           For k = 0 to n-1:   // Summation index
               C[j][i] = C[j][i] + A[k][i] * B[j][k]

7. For i = 0 to m-1:
       For j = 0 to p-1:
           Print C[j][i]       // Transpose access to print row-wise
```


---

## Code

```
#include <iostream>
#include <ctime>
#include <cstdlib> 

using namespace std;

int main(void)
{
    int m_npk, n_npk, p_npk;

    cout << "Enter m n p (A: m x n, B: n x p): ";
    cin >> m_npk >> n_npk >> p_npk;

    int **A_npk = (int **)malloc(m_npk * sizeof(int *));
    int **B_npk = (int **)malloc(n_npk * sizeof(int *));
    int **C_npk = (int **)malloc(m_npk * sizeof(int *));

    for (int i = 0; i < m_npk; ++i)
        A_npk[i] = (int *)malloc(n_npk * sizeof(int));

    for (int i = 0; i < n_npk; ++i)
        B_npk[i] = (int *)malloc(p_npk * sizeof(int));

    for (int i = 0; i < m_npk; ++i)
        C_npk[i] = (int *)malloc(p_npk * sizeof(int));

    for (int i = 0; i < m_npk; ++i)
        for (int j = 0; j < n_npk; ++j)
            A_npk[i][j] = rand() % 10;

    for (int i = 0; i < n_npk; ++i)
        for (int j = 0; j < p_npk; ++j)
            B_npk[i][j] = rand() % 10;

    for (int i = 0; i < m_npk; ++i)
        for (int j = 0; j < p_npk; ++j)
            C_npk[i][j] = 0;

    clock_t start_row_npk = clock();
    for (int i = 0; i < m_npk; ++i)
    {
        for (int k = 0; k < n_npk; ++k)
        {
            int temp_npk = A_npk[i][k];
            for (int j = 0; j < p_npk; ++j)
            {
                C_npk[i][j] += temp_npk * B_npk[k][j];
            }
        }
    }
    clock_t end_row_npk = clock();
    double time_row_major_npk = (double)(end_row_npk - start_row_npk) * 1000 / CLOCKS_PER_SEC;

    cout << "\nResult of matrix multiplication (Row-major order):\n";
    for (int i = 0; i < m_npk; ++i)
    {
        for (int j = 0; j < p_npk; ++j)
            cout << C_npk[i][j] << "\t";
        cout << "\n";
    }

    long long checksum_row_npk = 0;
    for (int i = 0; i < m_npk; ++i)
        for (int j = 0; j < p_npk; ++j)
            checksum_row_npk += C_npk[i][j];

    for (int i = 0; i < m_npk; ++i)
        for (int j = 0; j < p_npk; ++j)
            C_npk[i][j] = 0;

    clock_t start_col_npk = clock();
    for (int j = 0; j < p_npk; ++j)
    {
        for (int k = 0; k < n_npk; ++k)
        {
            int temp_npk = B_npk[k][j];
            for (int i = 0; i < m_npk; ++i)
            {
                C_npk[i][j] += A_npk[i][k] * temp_npk;
            }
        }
    }
    clock_t end_col_npk = clock();
    double time_col_major_npk = (double)(end_col_npk - start_col_npk) * 1000 / CLOCKS_PER_SEC;

    cout << "\nResult of matrix multiplication (Column-major order):\n";
    for (int i = 0; i < m_npk; ++i)
    {
        for (int j = 0; j < p_npk; ++j)
            cout << C_npk[j][i] << "\t";
        cout << "\n";
    }

    long long checksum_col_npk = 0;
    for (int i = 0; i < m_npk; ++i)
        for (int j = 0; j < p_npk; ++j)
            checksum_col_npk += C_npk[i][j];

    cout << "\nRow-major friendly access time: " << time_row_major_npk << " ms | Checksum: " << checksum_row_npk << endl;
    cout << "Column-major friendly access time: " << time_col_major_npk << " ms | Checksum: " << checksum_col_npk << endl;

    if (checksum_row_npk == checksum_col_npk)
        cout << "\n Matrix multiplication results match" << endl;
    else
        cout << "\n Matrix multiplication results differ" << endl;

    for (int i = 0; i < m_npk; ++i)
        free(A_npk[i]);
    for (int i = 0; i < n_npk; ++i)
        free(B_npk[i]);
    for (int i = 0; i < m_npk; ++i)
        free(C_npk[i]);

    free(A_npk);
    free(B_npk);
    free(C_npk);

    return 0;
}
```

---

## Output

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Row_Column.cpp -o Row_Column
 } ; if ($?) { .\Row_Column }
Enter m n p (A: m x n, B: n x p): 3 4 3

Result of matrix multiplication (Row-major order):
36      66      19
101     147     49
61      74      30

Result of matrix multiplication (Column-major order):
36      101     61
66      147     74
19      49      30

Row-major friendly access time: 0 ms | Checksum: 583
Column-major friendly access time: 0 ms | Checksum: 583

 Matrix multiplication results match