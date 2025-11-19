
---


# <center> ASSIGNMENT NO - 6 Unit_6 </center>

## Title :

**Simulate a faculty database as a hash table using the Divide hash function with linear probing and chaining without replacement method.**

---

## AIM

<p>To simulate a faculty database using the Divide hash function and handle collisions through linear probing with chaining without replacement.</p>

---

## OBJECTIVE

<p>To understand the concept of collision resolution using chaining without replacement in a hash table where each record points to the next node forming a chain.</p>

---

## THEORY

<p>Chaining without replacement maintains an array of records where collisions are handled using linked pointers within the same table.  
When a collision occurs, the new record is inserted in the next available free space and linked logically to the original position.</p>

---

## ALGORITHM

1. Initialize table with faculty records set to empty.
2. Use Divide method: `hash = key % size`.
3. If slot empty, insert record.
4. If collision, find next free slot and link current record’s chain to it.
5. For search, follow chain links until key found or chain ends.
6. Display the table.
7. End.

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

    int newIdx_npk = (idx_npk + 1) % SIZE;
    while (table_npk[newIdx_npk].occupied_npk && newIdx_npk != idx_npk)
        newIdx_npk = (newIdx_npk + 1) % SIZE;

    if (newIdx_npk == idx_npk) {
        cout << "Table Full\n";
        return;
    }

    table_npk[newIdx_npk] = {id_npk, name_npk, -1, true};
    int temp_npk = idx_npk;
    while (table_npk[temp_npk].link_npk != -1)
        temp_npk = table_npk[temp_npk].link_npk;
    table_npk[temp_npk].link_npk = newIdx_npk;
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
Enter ID and Name: 101 Prem

1.Insert 2.Display 3.Exit
Enter choice: 1
Enter ID and Name: 113 Lavanya

1.Insert 2.Display 3.Exit
Enter choice: 1
Enter ID and Name: 202 gauri

1.Insert 2.Display 3.Exit
Enter choice: 2
Index   ID      Name    Link
0       Empty
1       101     Prem    -1
2       202     gauri   -1
3       113     Lavanya -1
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

<p>The faculty database successfully demonstrated chaining without replacement using internal table links for collision handling.</p>

---



