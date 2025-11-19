---



# <center> ASSIGNMENT NO - 10 Unit_6 </center>

## Title :

**Design and implement a smart college placement portal using advanced hashing to manage student placement records with high performance and low collision probability under dynamic growth.**

---

## AIM

<p>To build a placement portal record system that supports fast insertion, search, update, and deletion using double hashing with dynamic resizing to maintain low collision probability as data grows.</p>

---

## OBJECTIVE

<p>The objective is to combine strong hashing and capacity management: apply double hashing for probe independence and rehash the table when the load factor exceeds a threshold, ensuring consistent performance.</p>

---

## THEORY

<p>Double hashing uses two independent hash functions to compute the probe step, reducing primary and secondary clustering. When the table’s load factor grows beyond a threshold, resizing and rehashing all entries restores sparsity, controlling collisions and maintaining performance over time.</p>

---

## ALGORITHM

1. Store records with fields: roll, name, branch, cgpa, status.
2. Use `h1 = roll % M` and `h2 = 1 + (roll % (M-1))`.
3. Probe by `idx = (h1 + k*h2) % M`.
4. Insert into first empty or deleted slot, update if key exists.
5. Search by repeating the same probe sequence until key or empty found.
6. Delete by marking a tombstone.
7. Maintain load factor; if it exceeds limit, resize to a larger prime and rehash all occupied entries.

---

## CODE

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

enum CellStateN_npk { E_NPK, O_NPK, D_NPK };

struct PlaceRec_npk {
    int roll_npk;
    string name_npk;
    string branch_npk;
    float cgpa_npk;
    string status_npk;
    CellStateN_npk state_npk;
};

bool isPrime_npk(int x_npk) {
    if (x_npk < 2) return false;
    if (x_npk % 2 == 0) return x_npk == 2;
    for (int d_npk = 3; d_npk * d_npk <= x_npk; d_npk += 2) if (x_npk % d_npk == 0) return false;
    return true;
}

int nextPrime_npk(int x_npk) {
    while (!isPrime_npk(x_npk)) x_npk++;
    return x_npk;
}

struct DHashTable_npk {
    vector<PlaceRec_npk> tab_npk;
    int M_npk;
    int used_npk;

    DHashTable_npk(int m_npk) { M_npk = nextPrime_npk(m_npk); tab_npk.assign(M_npk, {0,"","",0.0f,"",E_NPK}); used_npk = 0; }

    int h1_npk(int k_npk) { return k_npk % M_npk; }
    int h2_npk(int k_npk) { int r_npk = k_npk % (M_npk - 1); return 1 + r_npk; }

    double load_npk() { return double(used_npk) / double(M_npk); }

    void rehash_npk() {
        int newM_npk = nextPrime_npk(M_npk * 2 + 1);
        vector<PlaceRec_npk> old_npk = tab_npk;
        tab_npk.assign(newM_npk, {0,"","",0.0f,"",E_NPK});
        int oldM_npk = M_npk;
        M_npk = newM_npk;
        used_npk = 0;
        for (int i = 0; i < oldM_npk; i++) {
            if (old_npk[i].state_npk == O_NPK) {
                put_npk(old_npk[i].roll_npk, old_npk[i].name_npk, old_npk[i].branch_npk, old_npk[i].cgpa_npk, old_npk[i].status_npk);
            }
        }
    }

    void put_npk(int roll_npk, const string& name_npk, const string& branch_npk, float cgpa_npk, const string& status_npk) {
        if (load_npk() > 0.6) rehash_npk();
        int i1_npk = h1_npk(roll_npk);
        int i2_npk = h2_npk(roll_npk);
        int firstDel_npk = -1;
        for (int k = 0; k < M_npk; k++) {
            int idx_npk = (i1_npk + k * i2_npk) % M_npk;
            if (tab_npk[idx_npk].state_npk == O_NPK && tab_npk[idx_npk].roll_npk == roll_npk) {
                tab_npk[idx_npk].name_npk = name_npk;
                tab_npk[idx_npk].branch_npk = branch_npk;
                tab_npk[idx_npk].cgpa_npk = cgpa_npk;
                tab_npk[idx_npk].status_npk = status_npk;
                cout << "Updated at index " << idx_npk << endl;
                return;
            }
            if (tab_npk[idx_npk].state_npk == D_NPK && firstDel_npk == -1) firstDel_npk = idx_npk;
            if (tab_npk[idx_npk].state_npk == E_NPK) {
                int place_npk = (firstDel_npk != -1 ? firstDel_npk : idx_npk);
                tab_npk[place_npk] = {roll_npk, name_npk, branch_npk, cgpa_npk, status_npk, O_NPK};
                used_npk++;
                cout << "Inserted at index " << place_npk << endl;
                return;
            }
        }
        if (firstDel_npk != -1) {
            tab_npk[firstDel_npk] = {roll_npk, name_npk, branch_npk, cgpa_npk, status_npk, O_NPK};
            used_npk++;
            cout << "Inserted at index " << firstDel_npk << endl;
        } else {
            rehash_npk();
            put_npk(roll_npk, name_npk, branch_npk, cgpa_npk, status_npk);
        }
    }

    int findIndex_npk(int roll_npk) {
        int i1_npk = h1_npk(roll_npk);
        int i2_npk = h2_npk(roll_npk);
        for (int k = 0; k < M_npk; k++) {
            int idx_npk = (i1_npk + k * i2_npk) % M_npk;
            if (tab_npk[idx_npk].state_npk == E_NPK) return -1;
            if (tab_npk[idx_npk].state_npk == O_NPK && tab_npk[idx_npk].roll_npk == roll_npk) return idx_npk;
        }
        return -1;
    }

    void get_npk(int roll_npk) {
        int pos_npk = findIndex_npk(roll_npk);
        if (pos_npk == -1) cout << "Record not found\n";
        else cout << "Found -> Roll: " << tab_npk[pos_npk].roll_npk << ", Name: " << tab_npk[pos_npk].name_npk << ", Branch: " << tab_npk[pos_npk].branch_npk << ", CGPA: " << tab_npk[pos_npk].cgpa_npk << ", Status: " << tab_npk[pos_npk].status_npk << " at index " << pos_npk << endl;
    }

    void erase_npk(int roll_npk) {
        int pos_npk = findIndex_npk(roll_npk);
        if (pos_npk == -1) cout << "Record not found\n";
        else { tab_npk[pos_npk].state_npk = D_NPK; cout << "Deleted at index " << pos_npk << endl; }
    }

    void display_npk() {
        cout << "\nIndex\tState\tRoll\tName\tBranch\tCGPA\tStatus\n";
        for (int i = 0; i < M_npk; i++) {
            cout << i << "\t";
            if (tab_npk[i].state_npk == E_NPK) {
                cout << "EMPTY\n";
            } else if (tab_npk[i].state_npk == D_NPK) {
                cout << "DELETED\n";
            } else {
                cout << "OCCUPIED\t" << tab_npk[i].roll_npk << "\t" << tab_npk[i].name_npk << "\t" << tab_npk[i].branch_npk << "\t" << tab_npk[i].cgpa_npk << "\t" << tab_npk[i].status_npk << "\n";
            }
        }
        cout << "Capacity: " << M_npk << "  Used: " << used_npk << "  Load: " << load_npk() << endl;
    }
};

int main_npk() {
    DHashTable_npk ht_npk(11);
    while (true) {
        cout << "\n1.Insert/Update 2.Search 3.Delete 4.Display 5.Exit\nEnter choice: ";
        int ch_npk; cin >> ch_npk;
        if (ch_npk == 1) {
            int roll_npk; string name_npk, branch_npk, status_npk; float cgpa_npk;
            cout << "Enter Roll Name Branch CGPA Status: ";
            cin >> roll_npk >> name_npk >> branch_npk >> cgpa_npk >> status_npk;
            ht_npk.put_npk(roll_npk, name_npk, branch_npk, cgpa_npk, status_npk);
        } else if (ch_npk == 2) {
            int roll_npk; cout << "Enter Roll: "; cin >> roll_npk; ht_npk.get_npk(roll_npk);
        } else if (ch_npk == 3) {
            int roll_npk; cout << "Enter Roll: "; cin >> roll_npk; ht_npk.erase_npk(roll_npk);
        } else if (ch_npk == 4) {
            ht_npk.display_npk();
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

1.Insert/Update 2.Search 3.Delete 4.Display 5.Exit
Enter choice: 1
Enter Roll Name Branch CGPA Status: 101 Vani Mech 9.9 Placed
Inserted at index 2

1.Insert/Update 2.Search 3.Delete 4.Display 5.Exit
Enter choice: 1
Enter Roll Name Branch CGPA Status: 111 Nandini CS 9.2 Placed
Inserted at index 1

1.Insert/Update 2.Search 3.Delete 4.Display 5.Exit
Enter choice: 2
Enter Roll: 101
Found -> Roll: 101, Name: Vani, Branch: Mech, CGPA: 9.9, Status: Placed at index 2

1.Insert/Update 2.Search 3.Delete 4.Display 5.Exit
Enter choice: 4

Index   State   Roll    Name    Branch  CGPA    Status
0       EMPTY
1       OCCUPIED        111     Nandini CS      9.2     Placed
2       OCCUPIED        101     Vani    Mech    9.9     Placed
3       EMPTY
4       EMPTY
5       EMPTY
6       EMPTY
7       EMPTY
8       EMPTY
9       EMPTY
10      EMPTY
Capacity: 11  Used: 2  Load: 0.181818

1.Insert/Update 2.Search 3.Delete 4.Display 5.Exit
Enter choice:
```

---

## CONCLUSION

<p>The smart placement portal uses double hashing with dynamic resizing to sustain low collision probability and high performance under growth. It supports insertion, updates, search, deletion, and inspection of table load for robust management of placement data.</p>

---

