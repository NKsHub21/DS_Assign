# <center>ASSIGNMENT NO - 7 Unit_1</center>

## Title  
WAP to implement Bubble sort and Quick Sort on a 1D array of Student structure (contains student_name, student_roll_no, total_marks), with key as student_roll_no. And count the number of swap performed by each method.

---

### Theory: 

Bubble sort
Bubble Sort is a simple comparison-based sorting algorithm where adjacent elements are compared and swapped if they are in the wrong order. This process is repeated until the array is sorted.

       🔹 Why 'Bubble'?
            - Because the largest element “bubbles up” to its correct position in each pass.
          
        🔹Working Principle:
            - Each pass pushes the largest element to the rightmost side.
            - Repeat passes until the array is sorted.

        🔹 Time Complexity :  O(n²)
        🔹 Space Complexity:  O(1) (in-place sorting)

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

### Algorithm (Step-by-Step)

1.Start

2.Input the number of students size_npk.

3.Allocate memory dynamically for an array of Student_npk structures using malloc.

4.Each Student_npk has: student_name_npk, student_roll_no_npk, total_marks_npk.

5.Generate random students using generateRandomStudents_npk:

6.Assign random roll numbers (key for sorting).

7.Assign random marks.

8.Generate names like Student_1, Student_2….

9.Display original list using printStudents_npk.

10.Bubble Sort:

    Copy the student array to arrBubble_npk.

    Sort based on student_roll_no_npk.

    Count the number of swaps (bubbleSwaps_npk).

    Print the sorted list.

11.Quick Sort:

Copy the student array to arrQuick_npk.

Sort recursively using partitionArray_npk.

Count the number of swaps (quickSwaps_npk).

Print the sorted list.

Print total swap counts for both algorithms.

Free memory using free.

End

### Code
```
#include <iostream>
#include <cstdlib>
#include <cstring>
using namespace std;

struct Student_npk {
    char student_name_npk[50];
    int student_roll_no_npk;
    int total_marks_npk;
};

// Function prototypes
void generateRandomStudents_npk(Student_npk* arr_npk, int size_npk);
void printStudents_npk(Student_npk* arr_npk, int size_npk);
void bubbleSort_npk(Student_npk* arr_npk, int size_npk, int &swapCount_npk);
void quickSort_npk(Student_npk* arr_npk, int first_npk, int last_npk, int &swapCount_npk);
int  partitionArray_npk(Student_npk* arr_npk, int first_npk, int last_npk, int &swapCount_npk);
void swap_npk(Student_npk* s1_npk, Student_npk* s2_npk, int &swapCount_npk);

int main() {
    Student_npk* arr_npk = NULL;
    int size_npk;

    cout << "Enter the number of students: ";
    cin >> size_npk;

    arr_npk = (Student_npk*)malloc(sizeof(Student_npk) * size_npk);

    if (arr_npk == NULL) {
        cout << "Memory allocation failed.\n";
        exit(-1);
    }

    generateRandomStudents_npk(arr_npk, size_npk);

    cout << "\nOriginal Student List:\n";
    printStudents_npk(arr_npk, size_npk);

    // Bubble Sort
    Student_npk* arrBubble_npk = (Student_npk*)malloc(sizeof(Student_npk) * size_npk);
    memcpy(arrBubble_npk, arr_npk, sizeof(Student_npk) * size_npk);

    int bubbleSwaps_npk = 0;
    bubbleSort_npk(arrBubble_npk, size_npk, bubbleSwaps_npk);

    cout << "\nStudent List after Bubble Sort:\n";
    printStudents_npk(arrBubble_npk, size_npk);
    cout << "Total Swaps in Bubble Sort: " << bubbleSwaps_npk << "\n";

    // Quick Sort
    Student_npk* arrQuick_npk = (Student_npk*)malloc(sizeof(Student_npk) * size_npk);
    memcpy(arrQuick_npk, arr_npk, sizeof(Student_npk) * size_npk);

    int quickSwaps_npk = 0;
    quickSort_npk(arrQuick_npk, 0, size_npk - 1, quickSwaps_npk);

    cout << "\nStudent List after Quick Sort:\n";
    printStudents_npk(arrQuick_npk, size_npk);
    cout << "Total Swaps in Quick Sort: " << quickSwaps_npk << "\n";

    free(arr_npk);
    free(arrBubble_npk);
    free(arrQuick_npk);

    return 0;
}

void generateRandomStudents_npk(Student_npk* arr_npk, int size_npk) {
    for (int i_npk = 0; i_npk < size_npk; i_npk++) {
        sprintf(arr_npk[i_npk].student_name_npk, "Student_%d", i_npk + 1);
        arr_npk[i_npk].student_roll_no_npk = rand() % 100;
        arr_npk[i_npk].total_marks_npk = rand() % 500;
    }
}

void printStudents_npk(Student_npk* arr_npk, int size_npk) {
    cout << "Name\t\tRoll No\tMarks\n";
    cout << "----------------------------------\n";
    for (int i_npk = 0; i_npk < size_npk; i_npk++) {
        cout << arr_npk[i_npk].student_name_npk << "\t"
             << arr_npk[i_npk].student_roll_no_npk << "\t"
             << arr_npk[i_npk].total_marks_npk << "\n";
    }
}

void bubbleSort_npk(Student_npk* arr_npk, int size_npk, int &swapCount_npk) {
    int i_npk, j_npk;
    bool swapped_npk;
    for (i_npk = 0; i_npk < size_npk - 1; i_npk++) {
        swapped_npk = false;
        for (j_npk = 0; j_npk < size_npk - 1 - i_npk; j_npk++) {
            if (arr_npk[j_npk].student_roll_no_npk > arr_npk[j_npk + 1].student_roll_no_npk) {
                swap_npk(&arr_npk[j_npk], &arr_npk[j_npk + 1], swapCount_npk);
                swapped_npk = true;
            }
        }
        if (!swapped_npk) break;
    }
}

void quickSort_npk(Student_npk* arr_npk, int first_npk, int last_npk, int &swapCount_npk) {
    if (first_npk >= last_npk) return;
    int p_npk = partitionArray_npk(arr_npk, first_npk, last_npk, swapCount_npk);
    quickSort_npk(arr_npk, first_npk, p_npk - 1, swapCount_npk);
    quickSort_npk(arr_npk, p_npk + 1, last_npk, swapCount_npk);
}

int partitionArray_npk(Student_npk* arr_npk, int first_npk, int last_npk, int &swapCount_npk) {
    int pivot_npk = arr_npk[first_npk].student_roll_no_npk;
    int count_npk = 0;
    for (int i_npk = first_npk + 1; i_npk <= last_npk; i_npk++) {
        if (arr_npk[i_npk].student_roll_no_npk < pivot_npk) count_npk++;
    }
    int pivotIndex_npk = first_npk + count_npk;
    swap_npk(&arr_npk[pivotIndex_npk], &arr_npk[first_npk], swapCount_npk);

    int i_npk = first_npk, j_npk = last_npk;
    while (i_npk < pivotIndex_npk && j_npk > pivotIndex_npk) {
        while (arr_npk[i_npk].student_roll_no_npk < arr_npk[pivotIndex_npk].student_roll_no_npk) i_npk++;
        while (arr_npk[j_npk].student_roll_no_npk > arr_npk[pivotIndex_npk].student_roll_no_npk) j_npk--;
        if (i_npk < pivotIndex_npk && j_npk > pivotIndex_npk) {
            swap_npk(&arr_npk[i_npk], &arr_npk[j_npk], swapCount_npk);
            i_npk++;
            j_npk--;
        }
    }
    return pivotIndex_npk;
}

void swap_npk(Student_npk* s1_npk, Student_npk* s2_npk, int &swapCount_npk) {
    Student_npk temp_npk = *s1_npk;
    *s1_npk = *s2_npk;
    *s2_npk = temp_npk;
    swapCount_npk++;
}
```
### Output
```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_7.cpp -o Assign_7 } ; if ($?) { .\Assign_7 }
Enter the number of students: 4

Original Student List:
Name            Roll No Marks
----------------------------------
Student_1       41      467
Student_2       34      0
Student_3       69      224
Student_4       78      358

Student List after Bubble Sort:
Name            Roll No Marks
----------------------------------
Student_2       34      0
Student_1       41      467
Student_3       69      224
Student_4       78      358
Total Swaps in Bubble Sort: 1

Student List after Quick Sort:
Name            Roll No Marks
----------------------------------
Student_2       34      0
Student_1       41      467
Student_3       69      224
Student_4       78      358
Total Swaps in Quick Sort: 2
```