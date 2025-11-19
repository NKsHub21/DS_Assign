`Unit-IV_Assignment_3_BST_Min_Max.md`

# <center> ASSIGNMENT NO - 3 Unit_4 </center>

## Title :

**Write a Program to create a Binary Search Tree and find Minimum/Maximum in BST.**

---

## AIM

<p>To construct a BST and retrieve minimum and maximum values using boundary traversal.</p>

---

## OBJECTIVE

<p>Understand how the BST ordering enables O(h) retrieval of minimum and maximum by traversing extreme branches.</p>

---

## THEORY

<p>In a BST, the leftmost node holds the minimum key; the rightmost node holds the maximum. After constructing the tree via insertions that respect BST property, min and max are obtained by walking to the extreme left or right.</p>

---

## ALGORITHM

### Build and Query Min/Max

1. Insert keys into BST.
2. For minimum, follow `left` until `NULL`.
3. For maximum, follow `right` until `NULL`.
4. Print values.

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

int min_npk(Node_npk* root_npk) {
    if (root_npk == NULL) {
        cout << "Tree empty.\n";
        return -1;
    }
    while (root_npk->left_npk != NULL)
        root_npk = root_npk->left_npk;
    return root_npk->data_npk;
}

int max_npk(Node_npk* root_npk) {
    if (root_npk == NULL) {
        cout << "Tree empty.\n";
        return -1;
    }
    while (root_npk->right_npk != NULL)
        root_npk = root_npk->right_npk;
    return root_npk->data_npk;
}

int main_npk() {
    Node_npk* root_npk = NULL;
    int choice_npk, value_npk;

    while (true) {
        cout << "\n--- BST Min/Max ---\n";
        cout << "1. Insert\n";
        cout << "2. Minimum\n";
        cout << "3. Maximum\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> choice_npk;

        if (choice_npk == 1) {
            cout << "Enter value: ";
            cin >> value_npk;
            root_npk = insert_npk(root_npk, value_npk);
        } else if (choice_npk == 2) {
            cout << "Min: " << min_npk(root_npk) << endl;
        } else if (choice_npk == 3) {
            cout << "Max: " << max_npk(root_npk) << endl;
        } else if (choice_npk == 4) {
            cout << "Exiting.\n";
            exit(0);
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
1
Enter value: 40
1
Enter value: 25
1
Enter value: 90
2
Min: 25
3
Max: 90
```

---

## CONCLUSION

<p>Minimum and maximum queries in a BST use simple boundary traversals and run efficiently in proportion to tree height.</p>

---
