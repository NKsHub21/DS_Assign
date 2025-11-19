---


# <center> ASSIGNMENT NO - 3 Unit_6 </center>

## Title :

**Implement collision resolution using linked lists.**

---

## AIM

<p>To design a hash table that resolves collisions by connecting colliding keys through linked lists.</p>

---

## OBJECTIVE

<p>To understand linked list–based storage at each hash index as a general method of handling hash collisions.</p>

---

## THEORY

<p>Linked lists allow storing an arbitrary number of entries at each hash index. Each node contains a key and a pointer to the next node. This avoids overflow and provides dynamic collision handling.</p>

---

## ALGORITHM

1. Initialize hash table with NULL heads.
2. Compute index = hash(key).
3. Insert key at end of list at that index.
4. For search, traverse the list.
5. Display table.

---

## CODE

```cpp
#include <iostream>
#include <vector>
using namespace std;

struct Node_npk {
    int data_npk;
    Node_npk* next_npk;
};

#define SIZE 10

int hashFunc_npk(int key_npk) { return key_npk % SIZE; }

void insert_npk(vector<Node_npk*>& table_npk, int key_npk) {
    int idx_npk = hashFunc_npk(key_npk);
    Node_npk* newNode_npk = new Node_npk{key_npk, nullptr};
    if (!table_npk[idx_npk]) table_npk[idx_npk] = newNode_npk;
    else {
        Node_npk* temp_npk = table_npk[idx_npk];
        while (temp_npk->next_npk) temp_npk = temp_npk->next_npk;
        temp_npk->next_npk = newNode_npk;
    }
}

void display_npk(vector<Node_npk*>& table_npk) {
    for (int i = 0; i < SIZE; i++) {
        cout << i << " : ";
        Node_npk* t_npk = table_npk[i];
        while (t_npk) { cout << t_npk->data_npk << " -> "; t_npk = t_npk->next_npk; }
        cout << "NULL\n";
    }
}

int main_npk() {
    vector<Node_npk*> table_npk(SIZE, nullptr);
    int choice_npk, key_npk;
    while (true) {
        cout << "\n1.Insert 2.Display 3.Exit\nEnter choice: ";
        cin >> choice_npk;
        if (choice_npk == 1) {
            cout << "Enter key: "; cin >> key_npk;
            insert_npk(table_npk, key_npk);
        } else if (choice_npk == 2) display_npk(table_npk);
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
Enter key: 11

1.Insert 2.Display 3.Exit
Enter choice: 1
Enter key: 13

1.Insert 2.Display 3.Exit
Enter choice: 1
Enter key: 23

1.Insert 2.Display 3.Exit
Enter choice: 1
Enter key: 43

1.Insert 2.Display 3.Exit
Enter choice: 2
0 : NULL
1 : 11 -> NULL
2 : NULL
3 : 13 -> 23 -> 43 -> NULL
4 : NULL
5 : NULL
6 : NULL
7 : NULL
8 : NULL
9 : NULL

1.Insert 2.Display 3.Exit
Enter choice:
```

---

## CONCLUSION

<p>Linked list–based collision resolution allowed dynamic handling of multiple entries per hash index, enabling flexible hash table expansion.</p>

---

