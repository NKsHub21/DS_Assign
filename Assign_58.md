---



# <center> ASSIGNMENT NO - 8 Unit_6 </center>

## Title :

**Simulate an employee database using hash table and Mid-Square hashing with linear probing.**

---

## AIM

<p>To implement an employee database using a hash table with the mid-square hashing technique for key distribution.</p>

---

## OBJECTIVE

<p>To understand how the mid-square method generates uniformly distributed hash values by squaring the key and extracting middle digits.</p>

---

## THEORY

<p>The mid-square method squares the key and extracts the middle digits to compute the hash index.  
Collisions are resolved using linear probing.</p>

---

## ALGORITHM

1. Compute `hash = (key² / 10) % size`.
2. If slot empty, insert record.
3. If collision, probe sequentially.
4. For search, use same probing logic.
5. Display table contents.</p>

---

## CODE

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

#define SIZE 10

struct Employee_npk {
    int id_npk;
    string name_npk;
    bool occupied_npk;
};

int midSquareHash_npk(int key_npk) {
    int square_npk = key_npk * key_npk;
    int mid_npk = (square_npk / 10) % SIZE;
    return mid_npk;
}

void insert_npk(vector<Employee_npk>& table_npk, int id_npk, string name_npk) {
    int idx_npk = midSquareHash_npk(id_npk);
    int start_npk = idx_npk;
    do {
        if (!table_npk[idx_npk].occupied_npk) {
            table_npk[idx_npk] = {id_npk, name_npk, true};
            cout << "Inserted at index " << idx_npk << endl;
            return;
        }
        idx_npk = (idx_npk + 1) % SIZE;
    } while (idx_npk != start_npk);
    cout << "Table Full\n";
}

void display_npk(vector<Employee_npk>& table_npk) {
    for (int i = 0; i < SIZE; i++) {
        if (table_npk[i].occupied_npk)
            cout << i << " -> ID: " << table_npk[i].id_npk << ", Name: " << table_npk[i].name_npk << endl;
        else
            cout << i << " -> Empty\n";
    }
}

int main_npk() {
    vector<Employee_npk> table_npk(SIZE, {0, "", false});
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
Enter ID and Name: 101
IShan
Inserted at index 0

1.Insert 2.Display 3.Exit
Enter choice: 1
Enter ID and Name: 1
Iran
Inserted at index 1

1.Insert 2.Display 3.Exit
Enter choice: 2
0 -> ID: 101, Name: IShan
1 -> ID: 1, Name: Iran
2 -> Empty
3 -> Empty
4 -> Empty
5 -> Empty
6 -> Empty
7 -> Empty
8 -> Empty
9 -> Empty

1.Insert 2.Display 3.Exit
Enter choice:
```

---

## CONCLUSION

<p>The mid-square hashing technique provided uniform key distribution, and linear probing resolved collisions effectively in the employee database system.</p>

---