---



# <center> ASSIGNMENT NO - 5 Unit_6 </center>

## Title :

**Simulate a faculty database as a hash table. Search a particular faculty using MOD as hash function for linear probing collision handling technique. Assume suitable data.**

---

## AIM

<p>To implement a faculty database system using a hash table that stores and searches faculty details with MOD hash function and linear probing.</p>

---

## OBJECTIVE

<p>The goal is to simulate a faculty database using hash-based indexing with linear probing to handle collisions efficiently.</p>

---

## THEORY

<p>Each faculty record contains an ID, name, and department.  
The hash index is determined by `facultyID % tableSize`.  
If a collision occurs, linear probing searches sequentially for the next empty slot to insert or find records.</p>

---

## ALGORITHM

1. Initialize hash table with empty faculty records.
2. Define hash function as `id % size`.
3. For insertion, find the next free slot via linear probing.
4. For search, probe until the record is found or an empty slot is encountered.
5. Display all records.
6. End.

---

## CODE

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

#define SIZE 10

struct Faculty_npk {
    int id_npk;
    string name_npk;
    string dept_npk;
    bool occupied_npk;
};

int hashFunc_npk(int key_npk) { return key_npk % SIZE; }

void insert_npk(vector<Faculty_npk>& table_npk, int id_npk, string name_npk, string dept_npk) {
    int idx_npk = hashFunc_npk(id_npk);
    int start_npk = idx_npk;
    do {
        if (!table_npk[idx_npk].occupied_npk) {
            table_npk[idx_npk] = {id_npk, name_npk, dept_npk, true};
            cout << "Inserted at index " << idx_npk << endl;
            return;
        }
        idx_npk = (idx_npk + 1) % SIZE;
    } while (idx_npk != start_npk);
    cout << "Table Full\n";
}

void search_npk(vector<Faculty_npk>& table_npk, int id_npk) {
    int idx_npk = hashFunc_npk(id_npk);
    int start_npk = idx_npk;
    do {
        if (table_npk[idx_npk].occupied_npk && table_npk[idx_npk].id_npk == id_npk) {
            cout << "Found -> ID: " << table_npk[idx_npk].id_npk << ", Name: " << table_npk[idx_npk].name_npk << ", Dept: " << table_npk[idx_npk].dept_npk << endl;
            return;
        }
        if (!table_npk[idx_npk].occupied_npk) break;
        idx_npk = (idx_npk + 1) % SIZE;
    } while (idx_npk != start_npk);
    cout << "Faculty not found\n";
}

void display_npk(vector<Faculty_npk>& table_npk) {
    cout << "\nFaculty Hash Table:\n";
    for (int i = 0; i < SIZE; i++) {
        if (table_npk[i].occupied_npk)
            cout << i << " -> ID: " << table_npk[i].id_npk << ", Name: " << table_npk[i].name_npk << ", Dept: " << table_npk[i].dept_npk << endl;
        else
            cout << i << " -> Empty\n";
    }
}

int main_npk() {
    vector<Faculty_npk> table_npk(SIZE, {0, "", "", false});
    int choice_npk, id_npk;
    string name_npk, dept_npk;

    while (true) {
        cout << "\n1.Insert 2.Search 3.Display 4.Exit\nEnter choice: ";
        cin >> choice_npk;
        if (choice_npk == 1) {
            cout << "Enter ID, Name, Dept: ";
            cin >> id_npk >> name_npk >> dept_npk;
            insert_npk(table_npk, id_npk, name_npk, dept_npk);
        } else if (choice_npk == 2) {
            cout << "Enter ID to search: ";
            cin >> id_npk;
            search_npk(table_npk, id_npk);
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
Enter ID, Name, Dept: 101
Opal IT
Inserted at index 1

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 1
Enter ID, Name, Dept: 111  Ish Sales
Inserted at index 2

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 1
Enter ID, Name, Dept: 112
Jayesh marketing
Inserted at index 3

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 3

Faculty Hash Table:
0 -> Empty
1 -> ID: 101, Name: Opal, Dept: IT
2 -> ID: 111, Name: Ish, Dept: Sales
3 -> ID: 112, Name: Jayesh, Dept: marketing
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

<p>The faculty database was implemented using a hash table with the MOD hash function and linear probing for collision resolution, ensuring efficient record management and search operations.</p>

---

