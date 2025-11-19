
# <center> ASSIGNMENT NO - 6 Unit_3 </center>

## Title :

Write a program to keep track of patients as they check into a medical clinic, assigning patients to doctors on a first-come, first-served basis using a queue implemented with an array.

---

## AIM

<p>To write a C++ program that simulates a queue system for patient management in a medical clinic, where patients are assigned to doctors on a first-come, first-served basis using a queue implemented with an array.</p>

---

## OBJECTIVE

<p>The objective of this assignment is to understand how the queue data structure can be used to manage real-world scheduling problems like patient registration and doctor assignment.  
This program demonstrates how enqueue and dequeue operations maintain the First-Come, First-Served (FCFS) order of service in a medical clinic scenario.</p>

---

## What is a Queue?

<p>A queue is a linear data structure that follows the **First-In, First-Out (FIFO)** principle, where the first element added to the queue is the first one to be removed.  
Queues are widely used in scheduling and resource allocation systems, such as CPU scheduling, printer spooling, and clinic patient management systems.</p>

---

## Algorithm

### Algorithm to Manage Patient Queue

```
1. Start
2. Initialize an empty queue (array)
3. For each patient arrival:
      a. If queue is not full, enqueue (add) the patient to the queue
      b. If queue is full, display "Queue is Full"
4. When a doctor becomes available:
      a. If queue is not empty, dequeue (remove) a patient from the front
      b. Display that the patient is assigned to the doctor
      c. If queue is empty, display "No patients waiting"
5. Allow the user to:
      a. Add a new patient
      b. Assign a patient to a doctor (dequeue)
      c. Check if the queue is full or empty
      d. Display all patients in queue
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
    return (rear_npk == SIZE_NPK - 1);
}

int isQueueEmpty_npk(int rear_npk, int front_npk) {
    return (rear_npk == -1 || front_npk > rear_npk);
}

int addPatient_npk(string queue_npk[], int* rear_npk, string name_npk) {
    if (isQueueFull_npk(*rear_npk)) {
        cout << "Clinic queue is full. Cannot add more patients.\n";
        return 0;
    }
    (*rear_npk)++;
    queue_npk[*rear_npk] = name_npk;
    return 1;
}

int assignDoctor_npk(string queue_npk[], int* front_npk, int* rear_npk, string* name_npk) {
    if (isQueueEmpty_npk(*rear_npk, *front_npk)) {
        cout << "No patients waiting to be assigned.\n";
        return 0;
    }

    *name_npk = queue_npk[*front_npk];
    (*front_npk)++;

    if (*front_npk > *rear_npk) {
        *front_npk = 0;
        *rear_npk = -1;
    }
    return 1;
}

void displayQueue_npk(string queue_npk[], int front_npk, int rear_npk) {
    if (rear_npk == -1 || front_npk > rear_npk) {
        cout << "No patients in the queue.\n";
        return;
    }

    cout << "Patients waiting (Front -> Rear): ";
    for (int i = front_npk; i <= rear_npk; i++) {
        cout << queue_npk[i] << " ";
    }
    cout << endl;
}

int main_npk() {
    string queue_npk[SIZE_NPK];
    int front_npk = 0, rear_npk = -1;
    int choice_npk, status_npk;
    string name_npk;

    while (true) {
        cout << "\n==== Medical Clinic Queue Menu ====\n";
        cout << "1. Add Patient (Enqueue)\n";
        cout << "2. Assign Doctor (Dequeue)\n";
        cout << "3. Check if Queue is Full\n";
        cout << "4. Check if Queue is Empty\n";
        cout << "5. Display Patient Queue\n";
        cout << "6. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice_npk;

        switch (choice_npk) {
        case 1:
            cout << "Enter patient name: ";
            cin >> name_npk;
            status_npk = addPatient_npk(queue_npk, &rear_npk, name_npk);
            if (status_npk == 1)
                cout << "Patient added successfully.\n";
            break;

        case 2:
            status_npk = assignDoctor_npk(queue_npk, &front_npk, &rear_npk, &name_npk);
            if (status_npk == 1)
                cout << "Doctor is now attending to patient: " << name_npk << endl;
            break;

        case 3:
            if (isQueueFull_npk(rear_npk))
                cout << "Clinic queue is FULL.\n";
            else
                cout << "Clinic queue is NOT Full.\n";
            break;

        case 4:
            if (isQueueEmpty_npk(rear_npk, front_npk))
                cout << "Clinic queue is EMPTY.\n";
            else
                cout << "Clinic queue is NOT Empty.\n";
            break;

        case 5:
            displayQueue_npk(queue_npk, front_npk, rear_npk);
            break;

        case 6:
            cout << "Exiting program. Thank you!\n";
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

==== Medical Clinic Queue Menu ====
1. Add Patient (Enqueue)
2. Assign Doctor (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Patient Queue
6. Exit
Enter your choice: 1
Enter patient name: Krish
Patient added successfully.

==== Medical Clinic Queue Menu ====
1. Add Patient (Enqueue)
2. Assign Doctor (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Patient Queue
6. Exit
Enter your choice: 2
Doctor is now attending to patient: Krish

==== Medical Clinic Queue Menu ====
1. Add Patient (Enqueue)
2. Assign Doctor (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Patient Queue
6. Exit
Enter your choice: 5
No patients in the queue.

==== Medical Clinic Queue Menu ====
1. Add Patient (Enqueue)
2. Assign Doctor (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Patient Queue
6. Exit
Enter your choice: 1
Enter patient name: Onkar
Patient added successfully.

==== Medical Clinic Queue Menu ====
1. Add Patient (Enqueue)
2. Assign Doctor (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Patient Queue
6. Exit
Enter your choice: 1
Enter patient name: latil
Patient added successfully.

==== Medical Clinic Queue Menu ====
1. Add Patient (Enqueue)
2. Assign Doctor (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Patient Queue
6. Exit
Enter your choice: 1
Enter patient name: yadav
Patient added successfully.

==== Medical Clinic Queue Menu ====
1. Add Patient (Enqueue)
2. Assign Doctor (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Patient Queue
6. Exit
Enter your choice: 1
Enter patient name: prabhakar
Patient added successfully.

==== Medical Clinic Queue Menu ====
1. Add Patient (Enqueue)
2. Assign Doctor (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Patient Queue
6. Exit
Enter your choice: 5
Patients waiting (Front -> Rear): Onkar latil yadav prabhakar 

==== Medical Clinic Queue Menu ====
1. Add Patient (Enqueue)
2. Assign Doctor (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Patient Queue
6. Exit
Enter your choice: 3s
Clinic queue is NOT Full.

==== Medical Clinic Queue Menu ====
1. Add Patient (Enqueue)
2. Assign Doctor (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Patient Queue
6. Exit
Enter your choice: 4
Clinic queue is NOT Empty.

==== Medical Clinic Queue Menu ====
1. Add Patient (Enqueue)
2. Assign Doctor (Dequeue)
3. Check if Queue is Full
4. Check if Queue is Empty
5. Display Patient Queue
6. Exit
Enter your choice:   
```

---

## Conclusion

<p>The program successfully implements a queue-based patient management system for a medical clinic.  
Patients are added to the queue in the order they arrive, ensuring fair and systematic doctor assignment on a first-come, first-served basis.  
The use of enqueue and dequeue operations effectively demonstrates the working of the FIFO principle using an array-based queue.</p>

---


