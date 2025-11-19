# <center> ASSIGNMENT NO - 7 Unit_4 </center>

## Title :

**Write a program to illustrate operations on a BST holding numeric keys. Menu: Insert, Delete, Find, Show.**

---

## AIM

<p>To implement a menu-driven BST that supports insert, delete, find, and display operations.</p>

---

## OBJECTIVE

<p>Enable interactive management of a BST and verify ordered output via inorder traversal.</p>

---

## THEORY

<p>BSTs support efficient ordered set operations. Insertion follows ordering, deletion handles three structural cases, search follows branch comparisons, and inorder traversal lists keys in ascending order.</p>

---

## ALGORITHM

### Menu Operations

1. Insert: position key recursively.
2. Delete: handle leaf, one-child, two-children (copy successor).
3. Find: compare and branch until found or null.
4. Show: inorder traversal.

---

## CODE

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

struct Node_npk {
    int data_npk;
    Node_npk* left_npk;
    Node_npk* right_npk;
};

Node_npk* newNode_npk(int value_npk) {
    Node_npk* t_npk = new Node_npk;
    if (t_npk == NULL) {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    t_npk->data_npk = value_npk;
    t_npk->left_npk = NULL;
    t_npk->right_npk = NULL;
    return t_npk;
}

Node_npk* insert_npk(Node_npk* root_npk, int value_npk) {
    if (root_npk == NULL)
        return newNode_npk(value_npk);
    if (value_npk < root_npk->data_npk)
        root_npk->left_npk = insert_npk(root_npk->left_npk, value_npk);
    else if (value_npk > root_npk->data_npk)
        root_npk->right_npk = insert_npk(root_npk->right_npk, value_npk);
    return root_npk;
}

Node_npk* minNode_npk(Node_npk* root_npk) {
    while (root_npk && root_npk->left_npk)
        root_npk = root_npk->left_npk;
    return root_npk;
}

Node_npk* delete_npk(Node_npk* root_npk, int value_npk) {
    if (root_npk == NULL)
        return root_npk;
    if (value_npk < root_npk->data_npk)
        root_npk->left_npk = delete_npk(root_npk->left_npk, value_npk);
    else if (value_npk > root_npk->data_npk)
        root_npk->right_npk = delete_npk(root_npk->right_npk, value_npk);
    else {
        if (root_npk->left_npk == NULL) {
            Node_npk* t_npk = root_npk->right_npk;
            delete root_npk;
            return t_npk;
        } else if (root_npk->right_npk == NULL) {
            Node_npk* t_npk = root_npk->left_npk;
            delete root_npk;
            return t_npk;
        } else {
            Node_npk* t_npk = minNode_npk(root_npk->right_npk);
            root_npk->data_npk = t_npk->data_npk;
            root_npk->right_npk = delete_npk(root_npk->right_npk, t_npk->data_npk);
        }
    }
    return root_npk;
}

bool find_npk(Node_npk* root_npk, int value_npk) {
    while (root_npk != NULL) {
        if (value_npk == root_npk->data_npk)
            return true;
        if (value_npk < root_npk->data_npk)
            root_npk = root_npk->left_npk;
        else
            root_npk = root_npk->right_npk;
    }
    return false;
}

void inorder_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return;
    inorder_npk(root_npk->left_npk);
    cout << root_npk->data_npk << " ";
    inorder_npk(root_npk->right_npk);
}

int main_npk() {
    Node_npk* root_npk = NULL;
    int choice_npk, value_npk;
    while (true) {
        cout << "\n1. Insert  2. Delete  3. Find  4. Show(Inorder)  5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice_npk;

        if (choice_npk == 1) {
            cout << "Enter value to insert: ";
            cin >> value_npk;
            root_npk = insert_npk(root_npk, value_npk);
        } 
        else if (choice_npk == 2) {
            cout << "Enter value to delete: ";
            cin >> value_npk;
            root_npk = delete_npk(root_npk, value_npk);
        } 
        else if (choice_npk == 3) {
            cout << "Enter value to find: ";
            cin >> value_npk;
            cout << (find_npk(root_npk, value_npk) ? "Found\n" : "Not Found\n");
        } 
        else if (choice_npk == 4) {
            cout << "Inorder Traversal: ";
            inorder_npk(root_npk);
            cout << endl;
        } 
        else if (choice_npk == 5) {
            cout << "Exiting...\n";
            break;
        } 
        else {
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

1. Insert  2. Delete  3. Find  4. Show(Inorder)  5. Exit
Enter your choice: 1
Enter value to insert: 21

1. Insert  2. Delete  3. Find  4. Show(Inorder)  5. Exit
Enter your choice: 1
Enter value to insert: 22

1. Insert  2. Delete  3. Find  4. Show(Inorder)  5. Exit
Enter your choice: 1
Enter value to insert: 34

1. Insert  2. Delete  3. Find  4. Show(Inorder)  5. Exit
Enter your choice: 1
Enter value to insert: 56

1. Insert  2. Delete  3. Find  4. Show(Inorder)  5. Exit
Enter your choice: 1
Enter value to insert: 76

1. Insert  2. Delete  3. Find  4. Show(Inorder)  5. Exit
Enter your choice: 1
Enter value to insert: 22

1. Insert  2. Delete  3. Find  4. Show(Inorder)  5. Exit
Enter your choice: 4
Inorder Traversal: 21 22 34 56 76 

1. Insert  2. Delete  3. Find  4. Show(Inorder)  5. Exit
Enter your choice: 3
Enter value to find: 24
Not Found

1. Insert  2. Delete  3. Find  4. Show(Inorder)  5. Exit
Enter your choice: 5
Exiting...
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## CONCLUSION

<p>A complete BST menu was built, demonstrating insertion, search, deletion, and sorted display.</p>

---