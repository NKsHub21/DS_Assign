---


# <center> ASSIGNMENT NO - 7 Unit_6 </center>

## Title :

**Simulate a faculty database as a hash table using MOD hash function with linear probing and chaining with replacement method.**

---

## AIM

<p>To simulate a faculty database using the MOD hash function and chaining with replacement for handling collisions efficiently.</p>

---

## OBJECTIVE

<p>To understand collision handling by rearranging misplaced records such that records belonging to the same home address remain linked.</p>

---

## THEORY

<p>In chaining with replacement, if a record’s home address collides with another’s, it replaces the record currently occupying its home position if the occupant is out of place, maintaining proper logical links.</p>

---

## ALGORITHM

1. Compute hash index = key % size.
2. If slot empty, insert directly.
3. If occupied by a record from another home, replace it and relocate the displaced record.
4. Maintain chain links between records sharing the same home index.
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
    int link_npk;
    bool occupied_npk;
};

int hashFunc_npk(int key_npk) { return key_npk % SIZE; }

void insert_npk(vector<Faculty_npk>& table_npk, int id_npk, string name_npk) {
    int idx_npk = hashFunc_npk(id_npk);
    if (!table_npk[idx_npk].occupied_npk) {
        table_npk[idx_npk] = {id_npk, name_npk, -1, true};
        return;
    }

    int home_npk = hashFunc_npk(table_npk[idx_npk].id_npk);
    if (home_npk != idx_npk) {
        Faculty_npk temp_npk = table_npk[idx_npk];
        table_npk[idx_npk] = {id_npk, name_npk, -1, true};
        insert_npk(table_npk, temp_npk.id_npk, temp_npk.name_npk);
    } else {
        int newIdx_npk = (idx_npk + 1) % SIZE;
        while (table_npk[newIdx_npk].occupied_npk && newIdx_npk != idx_npk)
            newIdx_npk = (newIdx_npk + 1) % SIZE;
        table_npk[newIdx_npk] = {id_npk, name_npk, -1, true};
        int t_npk = idx_npk;
        while (table_npk[t_npk].link_npk != -1)
            t_npk = table_npk[t_npk].link_npk;
        table_npk[t_npk].link_npk = newIdx_npk;
    }
}

void display_npk(vector<Faculty_npk>& table_npk) {
    cout << "Index\tID\tName\tLink\n";
    for (int i = 0; i < SIZE; i++) {
        if (table_npk[i].occupied_npk)
            cout << i << "\t" << table_npk[i].id_npk << "\t" << table_npk[i].name_npk << "\t" << table_npk[i].link_npk << endl;
        else
            cout << i << "\tEmpty\n";
    }
}

int main_npk() {
    vector<Faculty_npk> table_npk(SIZE, {0, "", -1, false});
    int id_npk, choice_npk;
    string name_npk;

    while (true) {
        cout << "\n1.Insert 2.Display 3.Exit\nEnter choice: ";
        cin >> choice_npk;
        if (choice_npk == 1) {
            cout << "Enter ID and Name: ";
            cin >> id_npk >> name_npk;
            insert_npk(table_npk, id_npk, name_npk);
        } else if (choice_npk == 2)
            display_npk(table_npk);
        else break;
    }
    return 0;
}

int main() { return main_npk(); }
```

---

## OUTPUT

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }

1.Insert 2.Display 3.Exit
Enter choice: 1
Enter ID and Name: 110 Uday

1.Insert 2.Display 3.Exit
Enter choice: 1
Enter ID and Name: 101 Revan

1.Insert 2.Display 3.Exit
Enter choice: 1
Enter ID and Name: 101 elvish

1.Insert 2.Display 3.Exit
Enter choice: 2
Index   ID      Name    Link
0       110     Uday    -1
1       101     Revan   2
2       101     elvish  -1
3       Empty
4       Empty
5       Empty
6       Empty
7       Empty
8       Empty
9       Empty

1.Insert 2.Display 3.Exit
Enter choice:
```

---

## CONCLUSION

<p>Chaining with replacement ensured efficient utilization of the hash table by maintaining logical order and proper replacement for misplaced records.</p>

---
