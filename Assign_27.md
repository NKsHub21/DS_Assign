# <center> ASSIGNMENT NO - 7 Unit_3 </center>

## Title :

Write a program for a Pizza Parlour accepting maximum n orders. Orders are served on an FCFS (First Come First Serve) basis. Once placed, an order cannot be cancelled.
Simulate the system using a **circular queue** in C++.

---

## AIM

<p>To write a C++ program that simulates a Pizza Parlour order system using a circular queue where customers’ orders are taken and served on a First-Come, First-Served basis.</p>

---

## OBJECTIVE

<p>The objective of this assignment is to understand the working of a **circular queue** and its application in managing real-life problems such as order and service management.  
This program demonstrates the use of enqueue and dequeue operations with circular indexing to efficiently manage orders in a limited queue space.</p>

---

## What is a Circular Queue?

<p>A circular queue is a linear data structure that overcomes the limitation of a regular queue by connecting the end of the queue back to the front, forming a circle.  
It is commonly used for scheduling, buffering, and resource allocation problems — such as in food delivery systems or restaurant order queues.</p>

---

## Algorithm

### Algorithm to Simulate Pizza Parlour Order System

```
1. Start
2. Initialize front and rear as -1
3. For every order:
      a. If queue is not full, add order (Enqueue)
      b. If queue is full, display “No more orders can be accepted”
4. When an order is served:
      a. Remove order from front (Dequeue)
      b. If queue becomes empty, reset front and rear to -1
5. Allow user to:
      a. Place new order
      b. Serve next order
      c. Check if queue is full or empty
      d. Display all current orders
6. End
```

---

## Code

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

#define SIZE_NPK 5

int isCQFull_npk(int front_npk, int rear_npk) {
    int nextRear_npk;
    if (rear_npk == SIZE_NPK - 1)
        nextRear_npk = 0;
    else
        nextRear_npk = rear_npk + 1;
    if (nextRear_npk == front_npk)
        return 1;
    else
        return 0;
}

int isCQEmpty_npk(int front_npk) {
    if (front_npk == -1)
        return 1;
    else
        return 0;
}

int enQueue_npk(int queue_npk[], int* front_npk, int* rear_npk, int value_npk) {
    if (isCQFull_npk(*front_npk, *rear_npk) == 1) {
        cout << "Cannot place more orders. Queue is FULL.\n";
        return 0;
    }
    if (*front_npk == -1) {
        *front_npk = 0;
        *rear_npk = 0;
    } else {
        if (*rear_npk == SIZE_NPK - 1)
            *rear_npk = 0;
        else
            *rear_npk = *rear_npk + 1;
    }
    queue_npk[*rear_npk] = value_npk;
    return 1;
}

int deQueue_npk(int queue_npk[], int* front_npk, int* rear_npk, int* value_npk) {
    if (isCQEmpty_npk(*front_npk) == 1) {
        cout << "No pending orders to serve.\n";
        return 0;
    }
    *value_npk = queue_npk[*front_npk];
    if (*front_npk == *rear_npk) {
        *front_npk = -1;
        *rear_npk = -1;
    } else {
        if (*front_npk == SIZE_NPK - 1)
            *front_npk = 0;
        else
            *front_npk = *front_npk + 1;
    }
    return 1;
}

void displayQueue_npk(int queue_npk[], int front_npk, int rear_npk) {
    if (front_npk == -1) {
        cout << "No orders in the queue.\n";
        return;
    }
    cout << "Current Orders (Front -> Rear): ";
    while (front_npk != rear_npk) {
        cout << queue_npk[front_npk] << " ";
        if (front_npk == SIZE_NPK - 1)
            front_npk = 0;
        else
            front_npk = front_npk + 1;
    }
    cout << queue_npk[rear_npk] << endl;
}

int main_npk() {
    int queue_npk[SIZE_NPK];
    int front_npk = -1, rear_npk = -1;
    int choice_npk, value_npk, status_npk;

    while (1) {
        cout << "\n==== Pizza Parlour Order System ====\n";
        cout << "1. Place Order (Enqueue)\n";
        cout << "2. Serve Order (Dequeue)\n";
        cout << "3. Check if Queue is Full\n";
        cout << "4. Check if Queue is Empty\n";
        cout << "5. Display Orders\n";
        cout << "6. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice_npk;

        switch (choice_npk) {
        case 1:
            cout << "Enter order number: ";
            cin >> value_npk;
            status_npk = enQueue_npk(queue_npk, &front_npk, &rear_npk, value_npk);
            if (status_npk == 1)
                cout << "Order " << value_npk << " placed successfully.\n";
            break;

        case 2:
            status_npk = deQueue_npk(queue_npk, &front_npk, &rear_npk, &value_npk);
            if (status_npk == 1)
                cout << "Order " << value_npk << " served successfully.\n";
            break;

        case 3:
            if (isCQFull_npk(front_npk, rear_npk))
                cout << "Queue is FULL.\n";
            else
                cout << "Queue is NOT Full.\n";
            break;

        case 4:
            if (isCQEmpty_npk(front_npk))
                cout << "Queue is EMPTY.\n";
            else
                cout << "Queue is NOT Empty.\n";
            break;

        case 5:
            displayQueue_npk(queue_npk, front_npk, rear_npk);
            break;

        case 6:
            cout << "Exiting... Thank you for visiting!\n";
            exit(0);

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

==== Pizza Parlour Order System ====
1. Place Order (Enqueue)
2. Serve Order (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Orders
6. Exit
Enter your choice: 1
Enter order number: 32
Order 32 placed successfully.

==== Pizza Parlour Order System ====
1. Place Order (Enqueue)
2. Serve Order (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Orders
6. Exit
Enter your choice: 1
Enter order number: 56
Order 56 placed successfully.

==== Pizza Parlour Order System ====
1. Place Order (Enqueue)
2. Serve Order (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Orders
6. Exit
Enter your choice: 1
Enter order number: 78
Order 78 placed successfully.

==== Pizza Parlour Order System ====
1. Place Order (Enqueue)
2. Serve Order (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Orders
6. Exit
Enter your choice: 2
Order 32 served successfully.

==== Pizza Parlour Order System ====
1. Place Order (Enqueue)
2. Serve Order (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Orders
6. Exit
Enter your choice: 3
Queue is NOT Full.

==== Pizza Parlour Order System ====
1. Place Order (Enqueue)
2. Serve Order (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Orders
6. Exit
Enter your choice: 4
Queue is NOT Empty.

==== Pizza Parlour Order System ====
1. Place Order (Enqueue)
2. Serve Order (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Orders
6. Exit
Enter your choice: 5
Current Orders (Front -> Rear): 56 78

==== Pizza Parlour Order System ====
1. Place Order (Enqueue)
2. Serve Order (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Orders
6. Exit
Enter your choice:
```

---

## Conclusion

<p>The program successfully simulates a Pizza Parlour order management system using a circular queue implemented with an array in C++.  
Orders are accepted on a First-Come, First-Served basis, ensuring fairness in serving.  
The program effectively demonstrates circular queue behavior and prevents wasted memory space when the queue wraps around.</p>

---

