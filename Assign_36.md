# <center> ASSIGNMENT NO - 6 Unit_4 </center>

## Title :

**Using trees, assign roll numbers to students as per previous year results; topper gets roll no. 1.**

---

## AIM

<p>To assign roll numbers based on descending marks using a tree and rank-order traversal.</p>

---

## OBJECTIVE

<p>Store students in a marks-ordered tree and allocate sequential roll numbers starting from 1 for highest marks.</p>

---

## THEORY

<p>By inserting students in a BST ordered by marks (higher scores to the left), a reverse-inorder traversal visits students in descending order, enabling rank-wise roll assignment.</p>

---

## ALGORITHM

### Assign Rolls by Marks

1. Insert records `(name, marks)` into BST, ordering higher marks to the left.
2. Traverse with reverse-inorder (left as higher) or customize to enforce descending order.
3. Increment a counter to assign roll numbers during the traversal.
4. Display assigned rolls with names and marks.

---

## CODE

```cpp
#include <iostream>
#include <string>
#include <cstdlib>
using namespace std;

struct Node_npk {
    string name_npk;
    int marks_npk;
    int roll_npk;
    Node_npk* left_npk;
    Node_npk* right_npk;
};

Node_npk* newNode_npk(const string& nm_npk, int mk_npk) {
    Node_npk* t_npk = new Node_npk;
    if (t_npk == NULL) {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    t_npk->name_npk = nm_npk;
    t_npk->marks_npk = mk_npk;
    t_npk->roll_npk = 0;
    t_npk->left_npk = NULL;
    t_npk->right_npk = NULL;
    return t_npk;
}

Node_npk* insert_npk(Node_npk* root_npk, const string& nm_npk, int mk_npk) {
    if (root_npk == NULL)
        return newNode_npk(nm_npk, mk_npk);
    if (mk_npk > root_npk->marks_npk)
        root_npk->left_npk = insert_npk(root_npk->left_npk, nm_npk, mk_npk);
    else
        root_npk->right_npk = insert_npk(root_npk->right_npk, nm_npk, mk_npk);
    return root_npk;
}

void assignRolls_npk(Node_npk* root_npk, int& cur_npk) {
    if (root_npk == NULL)
        return;
    assignRolls_npk(root_npk->left_npk, cur_npk);
    cur_npk++;
    root_npk->roll_npk = cur_npk;
    assignRolls_npk(root_npk->right_npk, cur_npk);
}

void show_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return;
    show_npk(root_npk->left_npk);
    cout << root_npk->roll_npk << " " << root_npk->name_npk << " " << root_npk->marks_npk << endl;
    show_npk(root_npk->right_npk);
}

int main_npk() {
    Node_npk* root_npk = NULL;
    int choice_npk, marks_npk, current_npk;
    string name_npk;

    while (true) {
        cout << "\n1. Add Student  2. Assign Rolls  3. Show  4. Exit\n";
        cin >> choice_npk;
        if (choice_npk == 1) {
            cout << "Name Marks: ";
            cin >> name_npk >> marks_npk;
            root_npk = insert_npk(root_npk, name_npk, marks_npk);
        } else if (choice_npk == 2) {
            current_npk = 0;
            assignRolls_npk(root_npk, current_npk);
            cout << "Rolls assigned.\n";
        } else if (choice_npk == 3) {
            show_npk(root_npk);
        } else if (choice_npk == 4) {
            break;
        } else {
            cout << "Invalid choice.\n";
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

1. Add Student  2. Assign Rolls  3. Show  4. Exit
1
Name Marks: Naina 45

1. Add Student  2. Assign Rolls  3. Show  4. Exit
1
Name Marks: Opal
67

1. Add Student  2. Assign Rolls  3. Show  4. Exit
1
Name Marks: ujval 65

1. Add Student  2. Assign Rolls  3. Show  4. Exit
3
0 Opal 67
0 ujval 65
0 Naina 45

1. Add Student  2. Assign Rolls  3. Show  4. Exit
2
Rolls assigned.

1. Add Student  2. Assign Rolls  3. Show  4. Exit
3
1 Opal 67
2 ujval 65
3 Naina 45

1. Add Student  2. Assign Rolls  3. Show  4. Exit
4
PS C:\Users\Nandini\Documents\DS_VIT> 
```

---

## CONCLUSION

<p>Roll numbers were assigned in descending marks order using a reverse-inorder traversal over a marks-ordered binary search tree.</p>

---