# <center>ASSIGNMENT NO - 8 Unit_1</center>

## Title  
Write a program to input marks of n students Sort the marks in ascending order using the Quick Sort algorithm without using built-in library functions and analyse the sorting algorithm pass by pass. Find the minimum and maximum marks using Divide and Conquer (recursively).

---

### Theory: 

Quick Sort:
 Quick Sort is a divide-and-conquer sorting algorithm. It selects a pivot element, partitions the array such that:
                - All elements smaller than the pivot go to the left,
                - All elements greater than the pivot go to the right.
            Then it recursively sorts the left and right parts.

        🔹 Invented By: Tony Hoare in 1959.
          
        🔹Working Principle:
            1) Choose a pivot element (commonly the first, last, or middle).
            2) Partition the array so that:
                - arr[left..pivot-1] < pivot
                - arr[pivot+1..right] > pivot
            3) Recursively apply the same logic on left and right subarrays.

        🔹 Time Complexity :  O(n log n)
        🔹 Space Complexity:  O(log n) (due to recursion stack)

---



# **Algorithm: Quick Sort with Min & Max using Divide and Conquer**

### Step 1: Start

### Step 2: Input `n` (number of students).

### Step 3: Input `n` student marks into an array `marks_npk[]`.

---

### **Quick Sort Algorithm**

#### Function: `quick_sort_npk(array, low, high)`

1. If `low < high`, then:

   * Call `partition_npk(array, low, high)` → returns `pivotIndex`.
   * Print the array (to show current pass).
   * Recursively call:

     * `quick_sort_npk(array, low, pivotIndex - 1)`
     * `quick_sort_npk(array, pivotIndex + 1, high)`

#### Function: `partition_npk(array, low, high)`

1. Select the **first element** as pivot → `pivot = array[low]`.
2. Set `i = low + 1`, `j = high`.
3. Repeat while `i <= j`:

   * Increment `i` until `array[i] > pivot`.
   * Decrement `j` until `array[j] <= pivot`.
   * If `i < j`, swap `array[i]` and `array[j]`.
4. Swap `array[low]` and `array[j]` (placing pivot in its correct position).
5. Return `j` (the new pivot index).

---

### **Finding Minimum and Maximum (Divide & Conquer)**

#### Function: `find_min_max_npk(array, low, high)`

1. If `low == high`, then:

   * Both min and max = `array[low]`.
2. Else if `high == low + 1`, then:

   * Compare two elements and assign min and max accordingly.
3. Else:

   * Find `mid = (low + high) / 2`.
   * Recursively find `(min1, max1)` from left half.
   * Recursively find `(min2, max2)` from right half.
   * Final min = minimum of `(min1, min2)`.
   * Final max = maximum of `(max1, max2)`.

---

### Step 4: Call `quick_sort_npk(marks_npk, 0, n-1)` to sort the array.

### Step 5: Call `find_min_max_npk(marks_npk, 0, n-1)` to find minimum and maximum marks.

### Step 6: Display sorted marks, minimum mark, and maximum mark.

### Step 7: Stop.

---





### Code
```
#include <iostream>
#include <cstdlib>
using namespace std;

// Function prototypes
void quickSort_npk(int* arr_npk, int first_npk, int last_npk, int pass_npk);
int partitionArray_npk(int* arr_npk, int first_npk, int last_npk);
void printArray_npk(int* arr_npk, int size_npk);
int findMin_npk(int* arr_npk, int first_npk, int last_npk);
int findMax_npk(int* arr_npk, int first_npk, int last_npk);

int main() {
    int* arr_npk = NULL;
    int size_npk;

    cout << "Enter the number of students: ";
    cin >> size_npk;

    // dynamic allocation
    arr_npk = (int*)malloc(sizeof(int) * size_npk);

    if (arr_npk == NULL) {
        cout << "Memory allocation failed.\n";
        exit(-1);
    }

    // Input marks
    cout << "Enter marks of " << size_npk << " students:\n";
    for (int i_npk = 0; i_npk < size_npk; i_npk++) {
        cin >> arr_npk[i_npk];
    }

    cout << "\nOriginal Marks:\n";
    printArray_npk(arr_npk, size_npk);

    // Quick Sort with pass by pass analysis
    cout << "\n--- Quick Sort Pass by Pass ---\n";
    quickSort_npk(arr_npk, 0, size_npk - 1, 1);

    cout << "\nSorted Marks (Ascending):\n";
    printArray_npk(arr_npk, size_npk);

    // Find min and max using divide and conquer
    int min_npk = findMin_npk(arr_npk, 0, size_npk - 1);
    int max_npk = findMax_npk(arr_npk, 0, size_npk - 1);

    cout << "\nMinimum Marks: " << min_npk << endl;
    cout << "Maximum Marks: " << max_npk << endl;

    free(arr_npk);
    return 0;
}

// Quick Sort implementation (exact logic from your given code)
void quickSort_npk(int* arr_npk, int first_npk, int last_npk, int pass_npk) {
    if (first_npk >= last_npk) return;

    int p_npk = partitionArray_npk(arr_npk, first_npk, last_npk);

    cout << "After Pass " << pass_npk << ": ";
    printArray_npk(arr_npk, last_npk - first_npk + 1);

    quickSort_npk(arr_npk, first_npk, p_npk - 1, pass_npk + 1);
    quickSort_npk(arr_npk, p_npk + 1, last_npk, pass_npk + 1);
}

// Partition function (your logic: pivot = first element)
int partitionArray_npk(int* arr_npk, int first_npk, int last_npk) {
    int pivot_npk = arr_npk[first_npk];
    int count_npk = 0;

    for (int i_npk = first_npk + 1; i_npk <= last_npk; i_npk++) {
        if (arr_npk[i_npk] < pivot_npk) count_npk++;
    }

    int pivotIndex_npk = first_npk + count_npk;

    // swap pivot into position
    int temp_npk = arr_npk[pivotIndex_npk];
    arr_npk[pivotIndex_npk] = arr_npk[first_npk];
    arr_npk[first_npk] = temp_npk;

    int i_npk = first_npk, j_npk = last_npk;
    while (i_npk < pivotIndex_npk && j_npk > pivotIndex_npk) {
        while (arr_npk[i_npk] < arr_npk[pivotIndex_npk]) i_npk++;
        while (arr_npk[j_npk] > arr_npk[pivotIndex_npk]) j_npk--;
        if (i_npk < pivotIndex_npk && j_npk > pivotIndex_npk) {
            int temp2_npk = arr_npk[i_npk];
            arr_npk[i_npk] = arr_npk[j_npk];
            arr_npk[j_npk] = temp2_npk;
            i_npk++;
            j_npk--;
        }
    }
    return pivotIndex_npk;
}

// Print array
void printArray_npk(int* arr_npk, int size_npk) {
    for (int i_npk = 0; i_npk < size_npk; i_npk++) {
        cout << arr_npk[i_npk] << " ";
    }
    cout << endl;
}

// Divide & Conquer to find minimum
int findMin_npk(int* arr_npk, int first_npk, int last_npk) {
    if (first_npk == last_npk) return arr_npk[first_npk];
    int mid_npk = (first_npk + last_npk) / 2;
    int leftMin_npk = findMin_npk(arr_npk, first_npk, mid_npk);
    int rightMin_npk = findMin_npk(arr_npk, mid_npk + 1, last_npk);
    return (leftMin_npk < rightMin_npk) ? leftMin_npk : rightMin_npk;
}

// Divide & Conquer to find maximum
int findMax_npk(int* arr_npk, int first_npk, int last_npk) {
    if (first_npk == last_npk) return arr_npk[first_npk];
    int mid_npk = (first_npk + last_npk) / 2;
    int leftMax_npk = findMax_npk(arr_npk, first_npk, mid_npk);
    int rightMax_npk = findMax_npk(arr_npk, mid_npk + 1, last_npk);
    return (leftMax_npk > rightMax_npk) ? leftMax_npk : rightMax_npk;
}

```
### Output

PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_8.cpp -o Assign_8 } ; if ($?) { .\Assign_8 }
Enter the number of students: 4
Enter marks of 4 students:
21 23 34 45

Original Marks:
21 23 34 45

--- Quick Sort Pass by Pass ---
After Pass 1: 21 23 34 45
After Pass 2: 21 23 34
After Pass 3: 21 23

Sorted Marks (Ascending):
21 23 34 45

Minimum Marks: 21
Maximum Marks: 45