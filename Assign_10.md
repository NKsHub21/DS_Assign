
# <center>ASSIGNMENT NO - 10 Unit_1</center>

## Title  
		Write a program to arrange the list of employees as per the average of their height and weight by using Merge and Selection sorting method. Analyse their time complexities and conclude which algorithm will take less time to sort the list. 	

---

### Theory: 

 What is Merge Sort?
            - Merge Sort is a recursive, comparison-based sorting algorithm that follows the divide-and-conquer approach. It divides the array into two halves, sorts each half recursively, and then merges them.

        🔹 Real-World Analogy:
            - It’s like sorting a hand of playing cards — one card at a time into the correct position.
          
        🔹Working Principle:
            - Divide: Recursively split the array into halves.
            - Conquer: Sort the subarrays.
            - Combine: Merge sorted subarrays into one.

        🔹 Time Complexity :  O(n log n)
        🔹 Space Complexity:  O(n) (due to temporary arrays during merge)

        What is Selection Sort? 
            - Selection Sort is a simple comparison-based sorting algorithm. It works by repeatedly finding the minimum element from the unsorted part and putting it at the beginning.

       🔹 How It Works:
            - Divide the array into two parts: sorted and unsorted.
            - Repeatedly select the minimum element from the unsorted portion and swap it with the first unsorted element.

        🔹 Time Complexity :  O(n²)
        🔹 Space Complexity:  O(1) (in-place sorting)



---

## **Algorithm: Sorting Employees by Average Height & Weight**

### **Input:**

* Number of employees `n`
* Each employee has `height` and `weight`

### **Output:**

* Employees sorted by `(height + weight) / 2` (average) using:

  * **Merge Sort**
  * **Selection Sort**
* Comparison of time complexities

---

### **Step 1 — Read Input**

1. Read integer `n` → number of employees.
2. Allocate memory for an array `Employee[n]` dynamically using `malloc`.

---

### **Step 2 — Generate Employees**

For each employee `i` from `0` to `n-1`:

1. Assign random `height` (e.g., `rand() % 100 + 100` → range 100–199).
2. Assign random `weight` (e.g., `rand() % 100 + 40` → range 40–139).
3. Compute `average = (height + weight) / 2`.

---

### **Step 3 — Print Employees**

For each employee:

* Print `height`, `weight`, and `average`.

---

### **Step 4 — Merge Sort**

#### **Algorithm for Merge Sort:**

1. If `first < last`:

   * Compute `mid = (first + last) / 2`.
   * Recursively call `mergeSort(arr, first, mid)`.
   * Recursively call `mergeSort(arr, mid + 1, last)`.
   * Call `merge(arr, first, mid, last)`.

#### **Merge Function:**

1. Create two temporary arrays:

   * `L = arr[first...mid]`
   * `R = arr[mid+1...last]`
2. Compare elements of `L` and `R` by `average`.
3. Place smaller average into `arr[k]`.
4. Copy remaining elements from `L` or `R` into `arr`.
5. Free memory of `L` and `R`.

---

### **Step 5 — Selection Sort**

#### **Algorithm for Selection Sort:**

1. For `i = 0` to `n-2`:

   * Set `minIndex = i`.
   * For `j = i+1` to `n-1`:

     * If `arr[j].average < arr[minIndex].average`, set `minIndex = j`.
   * Swap `arr[i]` with `arr[minIndex]`.

---

### **Step 6 — Print Sorted Lists**

1. After merge sort → print employees sorted by average.
2. After selection sort → print employees sorted by average.

---

### **Step 7 — Time Complexity Analysis**

* Merge Sort: `O(n log n)`
* Selection Sort: `O(n^2)`
* **Conclusion:**
  Merge Sort will be faster for larger lists of employees.

---

### **Step 8 — Free Memory**

* Free dynamically allocated array for employees.

---





### Code
```
#include <stdio.h>
#include <stdlib.h>

// Structure for Employee
typedef struct Employee_npk {
    float height_npk;
    float weight_npk;
    float avg_npk;  // average of height and weight
} Employee_npk;

// Function Declarations
void generateEmployees_npk(Employee_npk*, int);
void printEmployees_npk(Employee_npk*, int);
void mergeSort_npk(Employee_npk*, int, int);
void merge_npk(Employee_npk*, int, int, int);
void selectionSort_npk(Employee_npk*, int);

int main(void)
{
    int size_npk;
    Employee_npk* arr_npk = NULL;

    printf("Enter number of employees: ");
    scanf("%d", &size_npk);

    // Allocate memory
    arr_npk = (Employee_npk*)malloc(sizeof(Employee_npk) * size_npk);
    if (arr_npk == NULL) {
        printf("Memory allocation failed!\n");
        exit(-1);
    }

    // Generate random employees
    generateEmployees_npk(arr_npk, size_npk);

    printf("\nOriginal List of Employees (Height, Weight, Average):\n");
    printEmployees_npk(arr_npk, size_npk);

    // --- Merge Sort ---
    mergeSort_npk(arr_npk, 0, size_npk - 1);
    printf("\nEmployees Sorted by Merge Sort (by average):\n");
    printEmployees_npk(arr_npk, size_npk);

    // Generate again for fair comparison
    generateEmployees_npk(arr_npk, size_npk);

    // --- Selection Sort ---
    selectionSort_npk(arr_npk, size_npk);
    printf("\nEmployees Sorted by Selection Sort (by average):\n");
    printEmployees_npk(arr_npk, size_npk);

    free(arr_npk);
    arr_npk = NULL;

    printf("\nTime Complexity Analysis:\n");
    printf("Merge Sort: O(n log n)\n");
    printf("Selection Sort: O(n^2)\n");
    printf("=> Merge Sort is faster for large lists.\n");

    return 0;
}

// Generate Employees with random height & weight
void generateEmployees_npk(Employee_npk* arr_npk, int size_npk)
{
    for (int i_npk = 0; i_npk < size_npk; i_npk++) {
        arr_npk[i_npk].height_npk = (rand() % 100) + 100;  // height 100-199
        arr_npk[i_npk].weight_npk = (rand() % 100) + 40;   // weight 40-139
        arr_npk[i_npk].avg_npk = (arr_npk[i_npk].height_npk + arr_npk[i_npk].weight_npk) / 2.0;
    }
}

// Print Employees
void printEmployees_npk(Employee_npk* arr_npk, int size_npk)
{
    for (int i_npk = 0; i_npk < size_npk; i_npk++) {
        printf("Emp %d -> H: %.2f, W: %.2f, Avg: %.2f\n",
               i_npk + 1, arr_npk[i_npk].height_npk, arr_npk[i_npk].weight_npk, arr_npk[i_npk].avg_npk);
    }
}

// Merge Sort Functions
void mergeSort_npk(Employee_npk* arr_npk, int first_npk, int last_npk)
{
    if (first_npk < last_npk) {
        int mid_npk = (first_npk + last_npk) / 2;
        mergeSort_npk(arr_npk, first_npk, mid_npk);
        mergeSort_npk(arr_npk, mid_npk + 1, last_npk);
        merge_npk(arr_npk, first_npk, mid_npk, last_npk);
    }
}

void merge_npk(Employee_npk* arr_npk, int first_npk, int mid_npk, int last_npk)
{
    int len1_npk = mid_npk - first_npk + 1;
    int len2_npk = last_npk - mid_npk;

    Employee_npk* L_npk = (Employee_npk*)malloc(sizeof(Employee_npk) * len1_npk);
    Employee_npk* R_npk = (Employee_npk*)malloc(sizeof(Employee_npk) * len2_npk);

    if (L_npk == NULL || R_npk == NULL) {
        printf("Memory allocation failed in merge!\n");
        exit(-2);
    }

    for (int i_npk = 0; i_npk < len1_npk; i_npk++)
        L_npk[i_npk] = arr_npk[first_npk + i_npk];
    for (int j_npk = 0; j_npk < len2_npk; j_npk++)
        R_npk[j_npk] = arr_npk[mid_npk + 1 + j_npk];

    int i_npk = 0, j_npk = 0, k_npk = first_npk;

    while (i_npk < len1_npk && j_npk < len2_npk) {
        if (L_npk[i_npk].avg_npk < R_npk[j_npk].avg_npk) {
            arr_npk[k_npk] = L_npk[i_npk];
            i_npk++;
        } else {
            arr_npk[k_npk] = R_npk[j_npk];
            j_npk++;
        }
        k_npk++;
    }

    while (i_npk < len1_npk) {
        arr_npk[k_npk] = L_npk[i_npk];
        i_npk++;
        k_npk++;
    }

    while (j_npk < len2_npk) {
        arr_npk[k_npk] = R_npk[j_npk];
        j_npk++;
        k_npk++;
    }

    free(L_npk);
    free(R_npk);
}

// Selection Sort
void selectionSort_npk(Employee_npk* arr_npk, int size_npk)
{
    for (int i_npk = 0; i_npk < size_npk - 1; i_npk++) {
        int minIndex_npk = i_npk;

        for (int j_npk = i_npk + 1; j_npk < size_npk; j_npk++) {
            if (arr_npk[j_npk].avg_npk < arr_npk[minIndex_npk].avg_npk)
                minIndex_npk = j_npk;
        }

        if (minIndex_npk != i_npk) {
            Employee_npk temp_npk = arr_npk[i_npk];
            arr_npk[i_npk] = arr_npk[minIndex_npk];
            arr_npk[minIndex_npk] = temp_npk;
        }
    }
}


```
### Output
```

PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_10.cpp -o Assign_10 } ; if ($?) { .\Assign_10 }
Enter number of employees: 3

Original List of Employees (Height, Weight, Average):
Emp 1 -> H: 141.00, W: 107.00, Avg: 124.00
Emp 2 -> H: 134.00, W: 40.00, Avg: 87.00
Emp 3 -> H: 169.00, W: 64.00, Avg: 116.50

Employees Sorted by Merge Sort (by average):
Emp 1 -> H: 134.00, W: 40.00, Avg: 87.00
Emp 2 -> H: 169.00, W: 64.00, Avg: 116.50
Emp 3 -> H: 141.00, W: 107.00, Avg: 124.00

Employees Sorted by Selection Sort (by average):
Emp 1 -> H: 105.00, W: 85.00, Avg: 95.00
Emp 2 -> H: 162.00, W: 104.00, Avg: 133.00
Emp 3 -> H: 178.00, W: 98.00, Avg: 138.00

Time Complexity Analysis:
Merge Sort: O(n log n)
Selection Sort: O(n^2)
=> Merge Sort is faster for large lists.
```