# <center> ASSIGNMENT NO - 9 Unit_3 </center>

## Title :

Write a program to implement multiple queues i.e. two queues using array and perform following operations on it.
A. Add Queue
B. Delete from Queue
C. Display Queue

---

## AIM

<p>To write a C++ program that implements two separate queues using arrays and performs operations such as adding elements, deleting elements, and displaying the contents of each queue.</p>

---

## OBJECTIVE

<p>The objective of this assignment is to understand how multiple queues can be managed simultaneously using arrays.  
This program demonstrates enqueue, dequeue, and display operations applied independently to two queues.</p>

---

## What are Multiple Queues?

<p>Multiple queues are two or more queues maintained independently in the same program.  
They are often used in systems that require separate processing channels — for example, customer service counters or multi-line task processing.  
Each queue follows the FIFO (First-In, First-Out) principle.</p>

---

## Algorithm

### Algorithm to Implement Two Queues

```
1. Start
2. Initialize two queues: queue1 and queue2
3. For each queue:
      a. Enqueue - add element if queue is not full
      b. Dequeue - remove element if queue is not empty
      c. Display - print all elements from front to rear
4. Provide user a menu to select which queue to operate on and the desired operation.
5. Repeat operations until user exits.
6. End
```

---

## Code

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

#define SIZE_NPK 5

int isQueueFull_npk(int rear_npk) {
    if (rear_npk == SIZE_NPK - 1)
        return 1;
    else
        return 0;
}

int isQueueEmpty_npk(int rear_npk) {
    if (rear_npk == -1)
        return 1;
    else
        return 0;
}

int addQ_npk(int queue_npk[], int* rear_npk, int val_npk) {
    if (isQueueFull_npk(*rear_npk) == 1) {
        cout << "Queue is Full. Cannot add element.\n";
        return 0;
    }
    *rear_npk = *rear_npk + 1;
    queue_npk[*rear_npk] = val_npk;
    return 1;
}

int delQ_npk(int queue_npk[], int* front_npk, int* rear_npk, int* val_npk) {
    if (*rear_npk == -1 || *front_npk > *rear_npk) {
        cout << "Queue is Empty. Cannot remove element.\n";
        return 0;
    }
    *val_npk = queue_npk[*front_npk];
    *front_npk = *front_npk + 1;
    if (*front_npk > *rear_npk) {
        *front_npk = 0;
        *rear_npk = -1;
    }
    return 1;
}

void printQ_npk(int queue_npk[], int front_npk, int rear_npk) {
    if (rear_npk == -1) {
        cout << "Queue is Empty.\n";
        return;
    }
    cout << "Queue (Front -> Rear): ";
    for (int i = front_npk; i <= rear_npk; i++) {
        cout << queue_npk[i] << " ";
    }
    cout << endl;
}

int main_npk() {
    int queue1_npk[SIZE_NPK], queue2_npk[SIZE_NPK];
    int front1_npk = 0, rear1_npk = -1;
    int front2_npk = 0, rear2_npk = -1;
    int choice_npk, val_npk, status_npk, qchoice_npk;

    while (1) {
        cout << "\n==== Multiple Queue Menu ====\n";
        cout << "1. Add to Queue\n";
        cout << "2. Delete from Queue\n";
        cout << "3. Display Queue\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice_npk;

        if (choice_npk == 4) {
            cout << "Exiting program. Thank you!\n";
            exit(0);
        }

        cout << "Select Queue (1 or 2): ";
        cin >> qchoice_npk;

        int* queue_ptr_npk;
        int *front_ptr_npk, *rear_ptr_npk;

        if (qchoice_npk == 1) {
            queue_ptr_npk = queue1_npk;
            front_ptr_npk = &front1_npk;
            rear_ptr_npk = &rear1_npk;
        } else if (qchoice_npk == 2) {
            queue_ptr_npk = queue2_npk;
            front_ptr_npk = &front2_npk;
            rear_ptr_npk = &rear2_npk;
        } else {
            cout << "Invalid Queue Choice.\n";
            continue;
        }

        switch (choice_npk) {
        case 1:
            cout << "Enter value to enqueue: ";
            cin >> val_npk;
            status_npk = addQ_npk(queue_ptr_npk, rear_ptr_npk, val_npk);
            if (status_npk == 1)
                cout << "Element added successfully.\n";
            break;

        case 2:
            status_npk = delQ_npk(queue_ptr_npk, front_ptr_npk, rear_ptr_npk, &val_npk);
            if (status_npk == 1)
                cout << "Removed element: " << val_npk << endl;
            break;

        case 3:
            printQ_npk(queue_ptr_npk, *front_ptr_npk, *rear_ptr_npk);
            break;

        default:
            cout << "Invalid choice. Please try again.\n";
        }
    }
    return 0;
}

int main() {
    return main_npk();
}
```

---

## Output

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }

==== Multiple Queue Menu ====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter your choice: 1
Select Queue (1 or 2): 1
Enter value to enqueue: 23
Element added successfully.

==== Multiple Queue Menu ====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter your choice: 1
Select Queue (1 or 2): 1
Enter value to enqueue: 33
Element added successfully.

==== Multiple Queue Menu ====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter your choice: 1
Select Queue (1 or 2): 32
Invalid Queue Choice.

==== Multiple Queue Menu ====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter your choice: 4
Exiting program. Thank you!
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## Conclusion

<p>The program successfully implements two independent queues using arrays and performs enqueue, dequeue, and display operations for each queue separately.  
It demonstrates how multiple queues can be managed within the same system, with each maintaining its own front and rear pointers.</p>

---
