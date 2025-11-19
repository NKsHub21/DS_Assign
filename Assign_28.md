# <center> ASSIGNMENT NO - 8 Unit_3 </center>

## Title :

Write a program that maintains a queue of passengers waiting to see a ticket agent. The program user should be able to insert a new passenger at the rear of the queue, display the passenger at the front of the queue, or remove the passenger at the front of the queue. The program will display the number of passengers left in the queue just before it terminates.

---

## AIM

<p>To write a C++ program that maintains a queue of passengers waiting to see a ticket agent using an array and allows enqueue, dequeue, and display operations.</p>

---

## OBJECTIVE

<p>The objective of this assignment is to understand the working of the queue data structure and how it can be applied in real-life scenarios such as passenger management systems.  
This program demonstrates basic queue operations — insertion, deletion, and display — using an array implementation.</p>

---

## What is a Queue?

<p>A queue is a linear data structure that follows the First-In, First-Out (FIFO) principle.  
The first element inserted is the first one removed. Queues are widely used in scheduling and real-world line-up systems such as ticket counters, print queues, and CPU job scheduling.</p>

---

## Algorithm

### Algorithm for Passenger Queue Management

```
1. Start
2. Initialize front = 0, rear = -1
3. For each operation:
      a. To insert a passenger (enqueue):
             If queue is not full, add passenger at rear
      b. To remove a passenger (dequeue):
             If queue is not empty, remove passenger from front
      c. To display front passenger:
             Show element at front
      d. To display number of passengers:
             Count elements from front to rear
4. Repeat until user exits.
5. On exit, display total passengers remaining.
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

int isQueueEmpty_npk(int rear_npk, int front_npk) {
    if (rear_npk == -1 || front_npk > rear_npk)
        return 1;
    else
        return 0;
}

int addQ_npk(string queue_npk[], int* rear_npk, string val_npk) {
    if (isQueueFull_npk(*rear_npk) == 1) {
        cout << "Queue is Full. Cannot add passenger.\n";
        return 0;
    }
    *rear_npk = *rear_npk + 1;
    queue_npk[*rear_npk] = val_npk;
    return 1;
}

int delQ_npk(string queue_npk[], int* front_npk, int* rear_npk, string* val_npk) {
    if (isQueueEmpty_npk(*rear_npk, *front_npk) == 1) {
        cout << "Queue is Empty. No passengers to remove.\n";
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

void printQ_npk(string queue_npk[], int front_npk, int rear_npk) {
    if (rear_npk == -1 || front_npk > rear_npk) {
        cout << "Queue is Empty.\n";
        return;
    }
    cout << "Passengers in queue (Front -> Rear): ";
    for (int i = front_npk; i <= rear_npk; i++) {
        cout << queue_npk[i] << " ";
    }
    cout << endl;
}

int countPassengers_npk(int front_npk, int rear_npk) {
    if (rear_npk == -1 || front_npk > rear_npk)
        return 0;
    else
        return (rear_npk - front_npk + 1);
}

int main_npk() {
    string queue_npk[SIZE_NPK];
    int front_npk = 0, rear_npk = -1;
    int choice_npk, status_npk;
    string val_npk;

    while (1) {
        cout << "\n==== Passenger Queue Menu ====\n";
        cout << "1. Add Passenger (Enqueue)\n";
        cout << "2. Serve Passenger (Dequeue)\n";
        cout << "3. Display Front Passenger\n";
        cout << "4. Display All Passengers\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice_npk;

        switch (choice_npk) {
        case 1:
            cout << "Enter passenger name: ";
            cin >> val_npk;
            status_npk = addQ_npk(queue_npk, &rear_npk, val_npk);
            if (status_npk == 1)
                cout << "Passenger " << val_npk << " added successfully.\n";
            break;

        case 2:
            status_npk = delQ_npk(queue_npk, &front_npk, &rear_npk, &val_npk);
            if (status_npk == 1)
                cout << "Passenger " << val_npk << " served and removed from queue.\n";
            break;

        case 3:
            if (isQueueEmpty_npk(rear_npk, front_npk))
                cout << "Queue is Empty.\n";
            else
                cout << "Front Passenger: " << queue_npk[front_npk] << endl;
            break;

        case 4:
            printQ_npk(queue_npk, front_npk, rear_npk);
            break;

        case 5:
            cout << "Program terminated.\n";
            cout << "Total passengers left in queue: " << countPassengers_npk(front_npk, rear_npk) << endl;
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
==== Passenger Queue Menu ====
1. Add Passenger (Enqueue)
2. Serve Passenger (Dequeue)
3. Display Front Passenger
4. Display All Passengers
5. Exit
Enter your choice: 1
Enter passenger name: Nandini
Passenger Nandini added successfully.

Enter your choice: 1
Enter passenger name: Raj
Passenger Raj added successfully.

Enter your choice: 4
Passengers in queue (Front -> Rear): Nandini Raj

Enter your choice: 2
Passenger Nandini served and removed from queue.

Enter your choice: 3
Front Passenger: Raj

Enter your choice: 5
Program terminated.
Total passengers left in queue: 1
```

---

## Conclusion

<p>The program successfully maintains a queue of passengers waiting to see a ticket agent using an array-based queue implementation.  
It allows users to add new passengers, display the front passenger, and remove passengers from the queue.  
The program also displays the number of passengers left before termination, demonstrating queue operations in a real-world context.</p>

---
