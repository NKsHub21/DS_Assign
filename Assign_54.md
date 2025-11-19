
---



# <center> ASSIGNMENT NO - 4 Unit_6 </center>

## Title :

**Store and retrieve student records using roll numbers.**

---

## AIM

<p>To implement a hash table that stores student records using roll numbers as keys, supporting efficient insertion and search operations.</p>

---

## OBJECTIVE

<p>The objective is to understand how hashing can be applied to store and retrieve structured student data with roll numbers mapped to table indices using a hash function.</p>

---

## THEORY

<p>In this system, each student record (roll number, name, marks) is inserted into the hash table based on the hash value of the roll number.  
Collisions are resolved using linear probing to find the next empty slot.</p>

---

## ALGORITHM

1. Define a student structure containing roll number, name, and marks.
2. Initialize hash table with empty slots.
3. Compute index = roll_no % table_size.
4. If occupied, use linear probing to find an empty slot.
5. To search, repeat the same probe sequence until found or empty.
6. Display all student records.
7. End.

---

## CODE

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

#define SIZE 10

struct Student_npk {
    int roll_npk;
    string name_npk;
    float marks_npk;
    bool occupied_npk;
};

int hashFunc_npk(int key_npk) { return key_npk % SIZE; }

void insert_npk(vector<Student_npk>& table_npk, int roll_npk, string name_npk, float marks_npk) {
    int idx_npk = hashFunc_npk(roll_npk);
    int start_npk = idx_npk;
    do {
        if (!table_npk[idx_npk].occupied_npk) {
            table_npk[idx_npk].roll_npk = roll_npk;
            table_npk[idx_npk].name_npk = name_npk;
            table_npk[idx_npk].marks_npk = marks_npk;
            table_npk[idx_npk].occupied_npk = true;
            cout << "Record inserted at index " << idx_npk << endl;
            return;
        }
        idx_npk = (idx_npk + 1) % SIZE;
    } while (idx_npk != start_npk);
    cout << "Hash Table Full\n";
}

void search_npk(vector<Student_npk>& table_npk, int roll_npk) {
    int idx_npk = hashFunc_npk(roll_npk);
    int start_npk = idx_npk;
    do {
        if (table_npk[idx_npk].occupied_npk && table_npk[idx_npk].roll_npk == roll_npk) {
            cout << "Found -> Roll: " << table_npk[idx_npk].roll_npk << ", Name: " << table_npk[idx_npk].name_npk << ", Marks: " << table_npk[idx_npk].marks_npk << endl;
            return;
        }
        if (!table_npk[idx_npk].occupied_npk) break;
        idx_npk = (idx_npk + 1) % SIZE;
    } while (idx_npk != start_npk);
    cout << "Record not found\n";
}

void display_npk(vector<Student_npk>& table_npk) {
    cout << "\nHash Table Records:\n";
    for (int i = 0; i < SIZE; i++) {
        if (table_npk[i].occupied_npk)
            cout << i << " -> Roll: " << table_npk[i].roll_npk << ", Name: " << table_npk[i].name_npk << ", Marks: " << table_npk[i].marks_npk << endl;
        else
            cout << i << " -> Empty\n";
    }
}

int main_npk() {
    vector<Student_npk> table_npk(SIZE, {0, "", 0.0, false});
    int choice_npk, roll_npk;
    string name_npk;
    float marks_npk;

    while (true) {
        cout << "\n1.Insert 2.Search 3.Display 4.Exit\nEnter choice: ";
        cin >> choice_npk;
        if (choice_npk == 1) {
            cout << "Enter Roll No, Name, Marks: ";
            cin >> roll_npk >> name_npk >> marks_npk;
            insert_npk(table_npk, roll_npk, name_npk, marks_npk);
        } else if (choice_npk == 2) {
            cout << "Enter Roll No to search: ";
            cin >> roll_npk;
            search_npk(table_npk, roll_npk);
        } else if (choice_npk == 3) {
            display_npk(table_npk);
        } else break;
    }
    return 0;
}

int main() { return main_npk(); }
```

---

## OUTPUT

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 1
Enter Roll No, Name, Marks: 21 Krish 99
Record inserted at index 1

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 1
Enter Roll No, Name, Marks: 1
Riya 56
Record inserted at index 2

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 3

Hash Table Records:
0 -> Empty
1 -> Roll: 21, Name: Krish, Marks: 99
2 -> Roll: 1, Name: Riya, Marks: 56
3 -> Empty
4 -> Empty
5 -> Empty
6 -> Empty
7 -> Empty
8 -> Empty
9 -> Empty

1.Insert 2.Search 3.Display 4.Exit
Enter choice:
```

---

## CONCLUSION

<p>The student record hash table successfully demonstrated efficient data storage and retrieval using linear probing and modular hashing based on roll numbers.</p>

---

