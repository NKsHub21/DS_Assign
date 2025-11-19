

# <center> ASSIGNMENT NO - 2 Unit_4</center>

## Title :

**Write a program to perform Binary Search Tree (BST) operations: Count total nodes, Compute height of the BST, and Mirror image.**

---

## AIM

<p>To implement operations on a BST that count total nodes, compute its height, and generate its mirror image using recursive functions in C++.</p>

---

## OBJECTIVE

<p>The objective is to practice recursive algorithms on BSTs to compute structural properties and transform the tree. Students will implement counting nodes, measuring height, and creating a mirror by swapping child pointers.</p>

---

## THEORY

<p>A Binary Search Tree (BST) organizes data to enable efficient insert, find, and delete operations. Structural queries like counting nodes and computing height provide insights into its shape and balance. Mirroring exchanges left and right subtrees at every node, producing a symmetric structure with respect to the root. These operations are commonly expressed recursively due to the self-similar nature of trees.</p>

---

## ALGORITHM

### Count, Height, Mirror in a BST

1. Start.
2. Build BST using repeated insertions.
3. Count nodes: recursively return `1 + count(left) + count(right)`.
4. Height: if empty return `0`; else `1 + max(height(left), height(right))`.
5. Mirror: for each node, swap left and right, then recurse on children.
6. Provide menu to execute operations.
7. End.

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

int countNodes_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return 0;
    return 1 + countNodes_npk(root_npk->left_npk) + countNodes_npk(root_npk->right_npk);
}

int height_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return 0;
    int lh_npk = height_npk(root_npk->left_npk);
    int rh_npk = height_npk(root_npk->right_npk);
    return 1 + (lh_npk > rh_npk ? lh_npk : rh_npk);
}

void inorder_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return;
    inorder_npk(root_npk->left_npk);
    cout << root_npk->data_npk << " ";
    inorder_npk(root_npk->right_npk);
}

void mirror_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return;
    Node_npk* temp_npk = root_npk->left_npk;
    root_npk->left_npk = root_npk->right_npk;
    root_npk->right_npk = temp_npk;
    mirror_npk(root_npk->left_npk);
    mirror_npk(root_npk->right_npk);
}

int main_npk() {
    Node_npk* root_npk = NULL;
    int choice_npk, value_npk;

    while (true) {
        cout << "\n--- BST: Count, Height, Mirror ---\n";
        cout << "1. Insert\n";
        cout << "2. Count Nodes\n";
        cout << "3. Height\n";
        cout << "4. Mirror\n";
        cout << "5. Inorder Display\n";
        cout << "6. Exit\n";
        cout << "Enter choice: ";
        cin >> choice_npk;

        if (choice_npk == 1) {
            cout << "Enter value: ";
            cin >> value_npk;
            root_npk = insert_npk(root_npk, value_npk);
        } else if (choice_npk == 2) {
            cout << "Total Nodes: " << countNodes_npk(root_npk) << endl;
        } else if (choice_npk == 3) {
            cout << "Height: " << height_npk(root_npk) << endl;
        } else if (choice_npk == 4) {
            mirror_npk(root_npk);
            cout << "Tree mirrored.\n";
        } else if (choice_npk == 5) {
            inorder_npk(root_npk);
            cout << endl;
        } else if (choice_npk == 6) {
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
cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 1
Enter value: 21

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 1
Enter value: 2

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 1
Enter value: 34

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 1
Enter value: 25

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 1
Enter value: 11

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 1
Enter value: 21

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 1
Enter value: 22

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 2
Total Nodes: 6

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 3
Height: 4

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 4
Tree mirrored.

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 5
34 25 22 21 11 2 

--- BST: Count, Height, Mirror ---
1. Insert
2. Count Nodes
3. Height
4. Mirror
5. Inorder Display
6. Exit
Enter choice: 6
Exiting.
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## CONCLUSION

<p>The program computes node count and height of a BST and generates its mirror image. Recursive definitions map naturally onto tree structure, demonstrating clean and efficient implementations.</p>

---
