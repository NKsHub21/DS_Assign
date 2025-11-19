# <center>ASSIGNMENT NO - 9 Unit_1</center>

## Title  
		Write a program using Bubble sort algorithm, assign the roll nos. to the students of your class as per their previous years result. i.e. topper will be roll no. 1 and analyse the sorting algorithm pass by pass.	

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




### Algorithm: Bubble Sort Roll Number Assignment
Step 1: Start
Step 2: Input n_npk (number of students).
Step 3: Input n_npk marks into array marks_npk[].
Step 4: Assign original roll numbers roll_npk[i] = i + 1.
Bubble Sort Algorithm

Repeat for pass_npk = 0 to n_npk - 2:

For each pair (j_npk, j_npk+1):

If marks_npk[j_npk] < marks_npk[j_npk+1], then:

Swap marks_npk[j_npk] and marks_npk[j_npk+1].

Swap corresponding roll_npk[j_npk] and roll_npk[j_npk+1].

After each pass, display roll numbers and marks.

Step 5: After sorting, assign new roll numbers based on ranks:

Highest marks → Roll No. 1 (Topper).

Next highest → Roll No. 2.

Continue till Roll No. n_npk.

Step 6: Display final roll number assignment.
Step 7: Stop.

---
 ### Code
 #include <iostream>
using namespace std;

void bubble_sort_npk(int marks_npk[], int roll_npk[], int n_npk) {
    for (int pass_npk = 0; pass_npk < n_npk - 1; pass_npk++) {
        for (int j_npk = 0; j_npk < n_npk - pass_npk - 1; j_npk++) {
            if (marks_npk[j_npk] < marks_npk[j_npk + 1]) {  
                // Swap marks
                int temp_npk = marks_npk[j_npk];
                marks_npk[j_npk] = marks_npk[j_npk + 1];
                marks_npk[j_npk + 1] = temp_npk;

                // Swap roll numbers simultaneously
                temp_npk = roll_npk[j_npk];
                roll_npk[j_npk] = roll_npk[j_npk + 1];
                roll_npk[j_npk + 1] = temp_npk;
            }
        }

        // Display array after each pass
        cout << "Pass " << pass_npk + 1 << ": ";
        for (int k_npk = 0; k_npk < n_npk; k_npk++) {
            cout << "(" << roll_npk[k_npk] << ":" << marks_npk[k_npk] << ") ";
        }
        cout << endl;
    }
}

int main() {
    int n_npk;
    cout << "Enter number of students: ";
    cin >> n_npk;

    int marks_npk[n_npk], roll_npk[n_npk];

    cout << "Enter marks of " << n_npk << " students: ";
    for (int i_npk = 0; i_npk < n_npk; i_npk++) {
        cin >> marks_npk[i_npk];
        roll_npk[i_npk] = i_npk + 1; // Initially assign roll numbers 1..n
    }

    bubble_sort_npk(marks_npk, roll_npk, n_npk);

    cout << "\nFinal Roll Numbers as per ranks (Topper = Roll No. 1):\n";
    for (int i_npk = 0; i_npk < n_npk; i_npk++) {
        cout << "Roll " << i_npk + 1 << " → Marks: " << marks_npk[i_npk] 
             << " (Original Roll: " << roll_npk[i_npk] << ")" << endl;
    }

    return 0;
}

### Output

PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_9.cpp -o Assign_9 } ; if ($?) { .\Assign_9 }
Enter number of students: 3
Enter marks of 3 students: 23 34 21
Pass 1: (2:34) (1:23) (3:21) 
Pass 2: (2:34) (1:23) (3:21)

Final Roll Numbers as per ranks (Topper = Roll No. 1):
Roll 1 -> Marks: 34 (Original Roll: 2)
Roll 2 -> Marks: 23 (Original Roll: 1)
Roll 3 -> Marks: 21 (Original Roll: 3)
