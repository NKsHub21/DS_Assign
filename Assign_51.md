
---



# <center> ASSIGNMENT NO - 1 Unit_6 </center>

## Title :

**Implement a hash table with collision resolution using linear probing.**

---

## AIM

<p>To implement a hash table that resolves collisions through linear probing when multiple keys hash to the same index.</p>

---

## OBJECTIVE

<p>To learn and apply linear probing as an open addressing technique in hash table collision management and to understand its probing sequence behavior.</p>

---

## THEORY

<p>Hashing maps keys to table indices using a hash function. When a collision occurs (same index for different keys), <b>linear probing</b> searches sequentially for the next available empty slot.</p>

---

## ALGORITHM

1. Initialize hash table of fixed size with -1.
2. For each insertion, compute index = key % size.
3. If occupied, move sequentially `(index + 1) % size` until an empty slot is found.
4. For searching, traverse similarly until key found or empty cell encountered.
5. For deletion, mark slot as -1.
6. Display table.

---

## CODE

```cpp
#include <iostream>
#include <vector>
using namespace std;

#define SIZE 10

int hashFunc_npk(int key_npk) {
    return key_npk % SIZE;
}

void insert_npk(vector<int>& table_npk, int key_npk) {
    int idx_npk = hashFunc_npk(key_npk);
    int start_npk = idx_npk;
    do {
        if (table_npk[idx_npk] == -1) {
            table_npk[idx_npk] = key_npk;
            cout << "Inserted at index " << idx_npk << endl;
            return;
        }
        idx_npk = (idx_npk + 1) % SIZE;
    } while (idx_npk != start_npk);
    cout << "Table Full\n";
}

void search_npk(vector<int>& table_npk, int key_npk) {
    int idx_npk = hashFunc_npk(key_npk);
    int start_npk = idx_npk;
    do {
        if (table_npk[idx_npk] == key_npk) {
            cout << "Key found at index " << idx_npk << endl;
            return;
        }
        if (table_npk[idx_npk] == -1) break;
        idx_npk = (idx_npk + 1) % SIZE;
    } while (idx_npk != start_npk);
    cout << "Key not found\n";
}

void display_npk(vector<int>& table_npk) {
    cout << "Hash Table:\n";
    for (int i = 0; i < SIZE; i++) {
        cout << i << " : " << table_npk[i] << endl;
    }
}

int main_npk() {
    vector<int> table_npk(SIZE, -1);
    int choice_npk, key_npk;
    while (true) {
        cout << "\n1.Insert 2.Search 3.Display 4.Exit\nEnter choice: ";
        cin >> choice_npk;
        if (choice_npk == 1) {
            cout << "Enter key: "; cin >> key_npk;
            insert_npk(table_npk, key_npk);
        } else if (choice_npk == 2) {
            cout << "Enter key to search: "; cin >> key_npk;
            search_npk(table_npk, key_npk);
        } else if (choice_npk == 3) {
            display_npk(table_npk);
        } else break;
    }
    return 0;
}

int main() {
    return main_npk();
}
```

---

## OUTPUT

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 1
Enter key: 21
Inserted at index 1

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 1
Enter key: 23
Inserted at index 3

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 1
Enter key: 23
Inserted at index 4

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 3
Hash Table:
0 : -1
1 : 21
2 : -1
3 : 23
4 : 23
5 : -1
6 : -1
7 : -1
8 : -1
9 : -1

1.Insert 2.Search 3.Display 4.Exit
Enter choice:
```

---

## CONCLUSION

<p>Linear probing resolved hash collisions effectively by scanning sequentially for available slots, demonstrating open addressing in hash tables.</p>

---


