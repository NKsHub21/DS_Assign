---



# <center> ASSIGNMENT NO - 2 unit_6</center>

## Title :

**Implement collision handling using separate chaining.**

---

## AIM

<p>To handle hash table collisions using separate chaining with linked lists at each index.</p>

---

## OBJECTIVE

<p>To understand how separate chaining stores multiple entries at the same index using linked structures for efficient collision management.</p>

---

## THEORY

<p>Separate chaining uses linked lists for each table index. When multiple keys hash to the same index, they are appended to the list stored at that bucket.</p>

---

## ALGORITHM

1. Initialize array of linked lists.
2. Compute hash index = key % size.
3. Append key to the list at that index.
4. For search, traverse the linked list.
5. For display, print all lists.

---

## CODE

```cpp
#include <iostream>
using namespace std;

#define SIZE 10
#define MAX 20   // max elements per chain

// Hash table using 2D array
int hashTable_npk[SIZE][MAX];
int count_npk[SIZE];   // how many elements in each chain

int hashFunc_npk(int key_npk) {
    return key_npk % SIZE;
}

void insert_npk(int key_npk) {
    int idx = hashFunc_npk(key_npk);

    if (count_npk[idx] < MAX) {
        hashTable_npk[idx][count_npk[idx]] = key_npk;
        count_npk[idx]++;
    } else {
        cout << "Chain full! Cannot insert.\n";
    }
}

void search_npk(int key_npk) {
    int idx = hashFunc_npk(key_npk);

    for (int i = 0; i < count_npk[idx]; i++) {
        if (hashTable_npk[idx][i] == key_npk) {
            cout << "Found in index " << idx << endl;
            return;
        }
    }
    cout << "Not found\n";
}

void display_npk() {
    cout << "\nHash Table:\n";
    for (int i = 0; i < SIZE; i++) {
        cout << i << " : ";
        for (int j = 0; j < count_npk[i]; j++) {
            cout << hashTable_npk[i][j] << " -> ";
        }
        cout << "NULL\n";
    }
}

int main() {
    int ch_npk, key_npk;

    // initialize chain counts
    for (int i = 0; i < SIZE; i++)
        count_npk[i] = 0;

    while (true) {
        cout << "\n1.Insert 2.Search 3.Display 4.Exit\nEnter choice: ";
        cin >> ch_npk;

        if (ch_npk == 1) {
            cout << "Enter key: ";
            cin >> key_npk;
            insert_npk(key_npk);
        }
        else if (ch_npk == 2) {
            cout << "Enter key to search: ";
            cin >> key_npk;
            search_npk(key_npk);
        }
        else if (ch_npk == 3) {
            display_npk();
        }
        else break;
    }

    return 0;
}

```

---

## OUTPUT

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 1
Enter key: 21

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 1
Enter key: 20

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 1
Enter key: 11

1.Insert 2.Search 3.Display 4.Exit
Enter choice: 3

Hash Table:
0 : 20 -> NULL
1 : 21 -> 11 -> NULL
2 : NULL
3 : NULL
4 : NULL
5 : NULL
6 : NULL
7 : NULL
8 : NULL
9 : NULL

1.Insert 2.Search 3.Display 4.Exit
Enter choice:
```

---

## CONCLUSION

<p>Separate chaining managed collisions efficiently by linking colliding elements, demonstrating flexible and scalable hashing with linked lists.</p>

---
