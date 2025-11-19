
# <center> ASSIGNMENT NO - 10 Unit_3 </center>

## Title :

In a call center, customer calls are handled on a first-come, first-served basis. Implement a queue system using a linked list where:
● Each customer call is enqueued as it arrives.
● Customer service agents dequeue calls to assist customers.
● If there are no calls, the system waits.

---

## AIM

<p>To write a C++ program that simulates a call center queue system using a linked list where customer calls are added to the queue as they arrive and are handled in the order they were received.</p>

---

## OBJECTIVE

<p>The objective of this assignment is to demonstrate the implementation of a queue using a linked list in C++.  
The program manages customer calls in a first-come, first-served manner using enqueue and dequeue operations.</p>

---

## What is a Linked List Queue?

<p>A queue implemented with a linked list uses dynamic memory allocation to store elements.  
Each node represents an element in the queue, containing data and a pointer to the next node.  
This allows flexible queue sizes without being restricted by array size limitations.</p>

---

## Algorithm

### Algorithm to Implement Call Center Queue System

```
1. Start
2. Create a linked list-based queue using dynamic memory allocation
3. For enqueue operation:
      a. Create a new node for each call
      b. Add it to the end of the queue
4. For dequeue operation:
      a. Remove the node at the front of the queue
      b. If the queue becomes empty, update front and rear to NULL
5. Display the queue at any point to show pending calls
6. Continue until the user chooses to exit
7. Before termination, free all allocated nodes
8. End
```

---

## Code

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

struct Node_npk {
    int data_npk;
    Node_npk* next_npk;
};

Node_npk* head_npk = NULL;
Node_npk* front_npk = NULL;
Node_npk* rear_npk = NULL;

Node_npk* getNode_npk(int value_npk) {
    Node_npk* newNode_npk = new Node_npk;
    if (newNode_npk == NULL) {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    newNode_npk->data_npk = value_npk;
    newNode_npk->next_npk = NULL;
    return newNode_npk;
}

void createQueue_npk() {
    head_npk = getNode_npk(-1);
    front_npk = NULL;
    rear_npk = NULL;
}

int isEmpty_npk() {
    if (front_npk == NULL)
        return 1;
    else
        return 0;
}

void enqueue_npk(int val_npk) {
    Node_npk* newNode_npk = getNode_npk(val_npk);
    if (isEmpty_npk()) {
        head_npk->next_npk = newNode_npk;
        front_npk = newNode_npk;
        rear_npk = newNode_npk;
    } else {
        rear_npk->next_npk = newNode_npk;
        rear_npk = newNode_npk;
    }
    cout << "Enqueued Call ID: " << val_npk << endl;
}

int dequeue_npk(int* val_npk) {
    if (isEmpty_npk()) {
        cout << "No calls waiting. Queue is EMPTY.\n";
        return 0;
    }
    Node_npk* temp_npk = front_npk;
    *val_npk = front_npk->data_npk;
    front_npk = front_npk->next_npk;
    head_npk->next_npk = front_npk;
    if (front_npk == NULL)
        rear_npk = NULL;
    delete temp_npk;
    return 1;
}

void display_npk() {
    if (isEmpty_npk()) {
        cout << "Queue is EMPTY.\n";
        return;
    }
    Node_npk* temp_npk = front_npk;
    cout << "Pending Calls (Front -> Rear): ";
    while (temp_npk != NULL) {
        cout << temp_npk->data_npk << " ";
        temp_npk = temp_npk->next_npk;
    }
    cout << endl;
}

void destroyQueue_npk() {
    Node_npk* temp_npk;
    while (head_npk != NULL) {
        temp_npk = head_npk;
        head_npk = head_npk->next_npk;
        delete temp_npk;
    }
    front_npk = NULL;
    rear_npk = NULL;
}

int main_npk() {
    createQueue_npk();
    int choice_npk, val_npk, result_npk;

    while (1) {
        cout << "\n==== Call Center Queue Menu ====\n";
        cout << "1. Add Customer Call (Enqueue)\n";
        cout << "2. Attend Next Call (Dequeue)\n";
        cout << "3. Check if Queue is Empty\n";
        cout << "4. Display Waiting Calls\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice_npk;

        switch (choice_npk) {
        case 1:
            cout << "Enter Call ID: ";
            cin >> val_npk;
            enqueue_npk(val_npk);
            break;

        case 2:
            result_npk = dequeue_npk(&val_npk);
            if (result_npk == 1)
                cout << "Attending Call ID: " << val_npk << endl;
            break;

        case 3:
            if (isEmpty_npk())
                cout << "Queue is EMPTY.\n";
            else
                cout << "Calls waiting in Queue.\n";
            break;

        case 4:
            display_npk();
            break;

        case 5:
            destroyQueue_npk();
            cout << "All calls cleared. Exiting system.\n";
            exit(0);

        default:
            cout << "Invalid choice. Try again.\n";
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
Invalid Queue Choice.

==== Multiple Queue Menu ====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter your choice: 4

==== Multiple Queue Menu ====
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter your choice: 4
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter your choice: 4
3. Display Queue
4. Exit
Enter your choice: 4
Enter your choice: 4
Exiting program. Thank you!
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }

==== Call Center Queue Menu ====
1. Add Customer Call (Enqueue)
2. Attend Next Call (Dequeue)
3. Check if Queue is Empty
4. Display Waiting Calls
5. Exit
Enter your choice: 1
Enter Call ID: 123
Enqueued Call ID: 123

==== Call Center Queue Menu ====
1. Add Customer Call (Enqueue)
2. Attend Next Call (Dequeue)
3. Check if Queue is Empty
4. Display Waiting Calls
5. Exit
Enter your choice: 1
Enter Call ID: 12345
Enqueued Call ID: 12345

==== Call Center Queue Menu ====
1. Add Customer Call (Enqueue)
2. Attend Next Call (Dequeue)
3. Check if Queue is Empty
4. Display Waiting Calls
5. Exit
Enter your choice: 1
Enter Call ID: 123456
Enqueued Call ID: 123456

==== Call Center Queue Menu ====
1. Add Customer Call (Enqueue)
2. Attend Next Call (Dequeue)
3. Check if Queue is Empty
4. Display Waiting Calls
5. Exit
Enter your choice: 2
Attending Call ID: 123

==== Call Center Queue Menu ====
1. Add Customer Call (Enqueue)
2. Attend Next Call (Dequeue)
3. Check if Queue is Empty
4. Display Waiting Calls
5. Exit
Enter your choice: 3
Calls waiting in Queue.

==== Call Center Queue Menu ====
1. Add Customer Call (Enqueue)
2. Attend Next Call (Dequeue)
3. Check if Queue is Empty
4. Display Waiting Calls
5. Exit
Enter your choice: 4
Pending Calls (Front -> Rear): 12345 123456 

==== Call Center Queue Menu ====
1. Add Customer Call (Enqueue)
2. Attend Next Call (Dequeue)
3. Check if Queue is Empty
4. Display Waiting Calls
5. Exit
Enter your choice: 5
All calls cleared. Exiting system.
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## Conclusion

<p>The program successfully simulates a call center queue system using a linked list in C++.  
Customer calls are added as they arrive (enqueue) and handled in order (dequeue).  
The program dynamically manages memory for each call, efficiently representing a real-world first-come, first-served system.</p>

---
