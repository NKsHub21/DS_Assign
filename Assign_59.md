

---



# <center> ASSIGNMENT NO - 9 Unit_6 </center>

## Title :

**WAP to simulate student databases as a hash table: implement efficient insertion, search, and deletion of student records.**

---

## AIM

<p>To design and implement a student database using hashing to support fast insertion, search, and deletion operations on student records.</p>

---

## OBJECTIVE

<p>The objective is to apply hashing with open addressing to store student records by roll number, while supporting search and deletion using probe sequences without breaking future lookups.</p>

---

## THEORY

<p>Hash tables provide average-case constant time operations by mapping keys to indices via a hash function. Open addressing with linear probing stores all records inside the table and probes sequentially when collisions occur. To support deletion without breaking search chains, cells use a tombstone marker so that probing continues past deleted slots when searching.</p>

---

## ALGORITHM

1. Initialize a fixed-size table with states: empty, occupied, deleted.
2. Compute index by `roll % size`.
3. Insertion probes forward until finding empty or deleted slot.
4. Search probes until key is found or an empty cell is encountered.
5. Deletion marks the found cell as deleted.
6. Display iterates all slots printing present records.

---

## CODE

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

#define SIZE 13

enum CellState_npk { EMPTY_NPK, OCCUPIED_NPK, DELETED_NPK };

struct Student_npk {
    int roll_npk;
    string name_npk;
    float marks_npk;
    CellState_npk state_npk;
};

int hash_npk(int key_npk) {
    return key_npk % SIZE;
}

int findIndex_npk(vector<Student_npk>& tab_npk, int roll_npk) {
    int idx_npk = hash_npk(roll_npk);
    int start_npk = idx_npk;
    do {
        if (tab_npk[idx_npk].state_npk == EMPTY_NPK) return -1;
        if (tab_npk[idx_npk].state_npk == OCCUPIED_NPK && tab_npk[idx_npk].roll_npk == roll_npk) return idx_npk;
        idx_npk = (idx_npk + 1) % SIZE;
    } while (idx_npk != start_npk);
    return -1;
}

void insert_npk(vector<Student_npk>& tab_npk, int roll_npk, const string& name_npk, float marks_npk) {
    int idx_npk = hash_npk(roll_npk);
    int start_npk = idx_npk;
    int firstDel_npk = -1;
    do {
        if (tab_npk[idx_npk].state_npk == OCCUPIED_NPK && tab_npk[idx_npk].roll_npk == roll_npk) {
            tab_npk[idx_npk].name_npk = name_npk;
            tab_npk[idx_npk].marks_npk = marks_npk;
            cout << "Updated at index " << idx_npk << endl;
            return;
        }
        if (tab_npk[idx_npk].state_npk == DELETED_NPK && firstDel_npk == -1) firstDel_npk = idx_npk;
        if (tab_npk[idx_npk].state_npk == EMPTY_NPK) {
            int place_npk = (firstDel_npk != -1 ? firstDel_npk : idx_npk);
            tab_npk[place_npk].roll_npk = roll_npk;
            tab_npk[place_npk].name_npk = name_npk;
            tab_npk[place_npk].marks_npk = marks_npk;
            tab_npk[place_npk].state_npk = OCCUPIED_NPK;
            cout << "Inserted at index " << place_npk << endl;
            return;
        }
        idx_npk = (idx_npk + 1) % SIZE;
    } while (idx_npk != start_npk);
    if (firstDel_npk != -1) {
        tab_npk[firstDel_npk].roll_npk = roll_npk;
        tab_npk[firstDel_npk].name_npk = name_npk;
        tab_npk[firstDel_npk].marks_npk = marks_npk;
        tab_npk[firstDel_npk].state_npk = OCCUPIED_NPK;
        cout << "Inserted at index " << firstDel_npk << endl;
    } else {
        cout << "Table Full\n";
    }
}

void search_npk(vector<Student_npk>& tab_npk, int roll_npk) {
    int pos_npk = findIndex_npk(tab_npk, roll_npk);
    if (pos_npk == -1) {
        cout << "Record not found\n";
    } else {
        cout << "Found -> Roll: " << tab_npk[pos_npk].roll_npk << ", Name: " << tab_npk[pos_npk].name_npk << ", Marks: " << tab_npk[pos_npk].marks_npk << " at index " << pos_npk << endl;
    }
}

void delete_npk(vector<Student_npk>& tab_npk, int roll_npk) {
    int pos_npk = findIndex_npk(tab_npk, roll_npk);
    if (pos_npk == -1) {
        cout << "Record not found\n";
    } else {
        tab_npk[pos_npk].state_npk = DELETED_NPK;
        cout << "Deleted at index " << pos_npk << endl;
    }
}

void display_npk(vector<Student_npk>& tab_npk) {
    cout << "\nIndex\tState\tRoll\tName\tMarks\n";
    for (int i = 0; i < SIZE; i++) {
        cout << i << "\t";
        if (tab_npk[i].state_npk == EMPTY_NPK) {
            cout << "EMPTY\n";
        } else if (tab_npk[i].state_npk == DELETED_NPK) {
            cout << "DELETED\n";
        } else {
            cout << "OCCUPIED\t" << tab_npk[i].roll_npk << "\t" << tab_npk[i].name_npk << "\t" << tab_npk[i].marks_npk << "\n";
        }
    }
}

int main_npk() {
    vector<Student_npk> tab_npk(SIZE, {0, "", 0.0f, EMPTY_NPK});
    int ch_npk;
    while (true) {
        cout << "\n1.Insert 2.Search 3.Delete 4.Display 5.Exit\nEnter choice: ";
        cin >> ch_npk;
        if (ch_npk == 1) {
            int r_npk; string n_npk; float m_npk;
            cout << "Enter Roll Name Marks: ";
            cin >> r_npk >> n_npk >> m_npk;
            insert_npk(tab_npk, r_npk, n_npk, m_npk);
        } else if (ch_npk == 2) {
            int r_npk;
            cout << "Enter Roll to search: ";
            cin >> r_npk;
            search_npk(tab_npk, r_npk);
        } else if (ch_npk == 3) {
            int r_npk;
            cout << "Enter Roll to delete: ";
            cin >> r_npk;
            delete_npk(tab_npk, r_npk);
        } else if (ch_npk == 4) {
            display_npk(tab_npk);
        } else {
            break;
        }
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
Enter choice: 2
0 -> ID: 101, Name: IShan
1 -> ID: 1, Name: Iran
2 -> Empty
3 -> Empty
4 -> Empty
5 -> Empty
6 -> Empty
3 -> Empty
4 -> Empty
5 -> Empty
6 -> Empty
7 -> Empty
8 -> Empty
9 -> Empty

7 -> Empty
8 -> Empty
9 -> Empty

1.Insert 2.Display 3.Exit
Enter choice: cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }

1.Insert 2.Search 3.Delete 4.Display 5.Exit
Enter choice: 1
Enter Roll Name Marks: 11 Kavya 67
Inserted at index 11

1.Insert 2.Search 3.Delete 4.Display 5.Exit
Enter choice: 1
Enter Roll Name Marks: 32 reval 77
Inserted at index 6

1.Insert 2.Search 3.Delete 4.Display 5.Exit
Enter choice: 1 
Enter Roll Name Marks: 45 ojas 23
Inserted at index 7

1.Insert 2.Search 3.Delete 4.Display 5.Exit
Enter choice:
2
Enter Roll to search: 67
Record not found

1.Insert 2.Search 3.Delete 4.Display 5.Exit
Enter choice: 2
Enter Roll to search: 11
Found -> Roll: 11, Name: Kavya, Marks: 67 at index 11

1.Insert 2.Search 3.Delete 4.Display 5.Exit
Enter choice: 4

Index   State   Roll    Name    Marks
0       EMPTY
1       EMPTY
2       EMPTY
3       EMPTY
4       EMPTY
5       EMPTY
6       OCCUPIED        32      reval   77
7       OCCUPIED        45      ojas    23
8       EMPTY
9       EMPTY
10      EMPTY
11      OCCUPIED        11      Kavya   67
12      EMPTY

1.Insert 2.Search 3.Delete 4.Display 5.Exit
Enter choice:
```

---

## CONCLUSION

<p>The student database uses open addressing with tombstones to support insertion, search, and deletion while preserving probe sequences, delivering fast average-case performance.</p>

---

