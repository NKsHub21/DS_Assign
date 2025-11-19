

`Unit-IV_Assignment_1_BST_Create_Insert_Delete_Levelwise.md`

---

# <center> ASSIGNMENT NO - 1 Unit_4 </center>

## Title :

**Write a program to perform Binary Search Tree (BST) operations — Create, Insert, Delete, and Level-wise Display.**

---

## AIM

<p>To write a C++ program that implements Binary Search Tree (BST) operations such as insertion, deletion, and level-wise display using linked structures.</p>

---

## OBJECTIVE

<p>The objective of this experiment is to understand the implementation of a Binary Search Tree (BST) and the various operations that can be performed on it.  
This includes dynamically inserting nodes, deleting nodes based on specific conditions, and displaying the tree in a level-wise manner using a queue.  
Through this program, students learn the concept of recursive and iterative traversals in trees and how the hierarchical structure supports efficient data organization.</p>

---

## THEORY

<p>A <b>Binary Search Tree (BST)</b> is a special type of binary tree in which each node contains a value such that:</p>  

<ul>
<li>All nodes in the left subtree contain values less than the root node’s value.</li>
<li>All nodes in the right subtree contain values greater than the root node’s value.</li>
</ul>

<p>This property ensures that searching, insertion, and deletion operations can be performed efficiently (in O(log n) average time).  
Level-wise display of a BST is performed using <b>Breadth-First Search (BFS)</b>, where each node of the tree is visited level by level using a queue.</p>

---

## ALGORITHM

### Algorithm to Perform BST Operations

1. **Start the program.**
2. Create a structure `Node` with members `data`, `left`, and `right`.
3. For insertion:

   * If the tree is empty, create a new node and make it the root.
   * Else, recursively insert the new key into the correct subtree (left or right).
4. For deletion:

   * Search for the node to be deleted.
   * Handle three cases:
     a. Node is a leaf.
     b. Node has one child.
     c. Node has two children (replace with inorder successor).
5. For level-wise display:

   * Use a queue to traverse the tree level by level.
   * Print nodes at each level sequentially.
6. Repeat operations as per user choice until exit.
7. **End the program.**

---

## CODE

```cpp
#include <iostream>
#include <queue>
#include <cstdlib>
using namespace std;

struct Node_npk {
    int data_npk;
    Node_npk* left_npk;
    Node_npk* right_npk;
};

Node_npk* newNode_npk(int value_npk) {
    Node_npk* temp_npk = new Node_npk;
    if (temp_npk == NULL) {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    temp_npk->data_npk = value_npk;
    temp_npk->left_npk = temp_npk->right_npk = NULL;
    return temp_npk;
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
    while (root_npk && root_npk->left_npk != NULL)
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
            Node_npk* temp_npk = root_npk->right_npk;
            delete root_npk;
            return temp_npk;
        }
        else if (root_npk->right_npk == NULL) {
            Node_npk* temp_npk = root_npk->left_npk;
            delete root_npk;
            return temp_npk;
        }
        Node_npk* temp_npk = minNode_npk(root_npk->right_npk);
        root_npk->data_npk = temp_npk->data_npk;
        root_npk->right_npk = delete_npk(root_npk->right_npk, temp_npk->data_npk);
    }
    return root_npk;
}

void levelwiseDisplay_npk(Node_npk* root_npk) {
    if (root_npk == NULL) {
        cout << "Tree is empty.\n";
        return;
    }

    queue<Node_npk*> q_npk;
    q_npk.push(root_npk);

    while (!q_npk.empty()) {
        int levelSize_npk = q_npk.size();
        while (levelSize_npk--) {
            Node_npk* current_npk = q_npk.front();
            q_npk.pop();
            cout << current_npk->data_npk << " ";
            if (current_npk->left_npk)
                q_npk.push(current_npk->left_npk);
            if (current_npk->right_npk)
                q_npk.push(current_npk->right_npk);
        }
        cout << endl;
    }
}

int main_npk() {
    Node_npk* root_npk = NULL;
    int choice_npk, value_npk;

    while (true) {
        cout << "\n--- Binary Search Tree Menu ---\n";
        cout << "1. Insert Node\n";
        cout << "2. Delete Node\n";
        cout << "3. Level-wise Display\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice_npk;

        switch (choice_npk) {
            case 1:
                cout << "Enter value to insert: ";
                cin >> value_npk;
                root_npk = insert_npk(root_npk, value_npk);
                break;
            case 2:
                cout << "Enter value to delete: ";
                cin >> value_npk;
                root_npk = delete_npk(root_npk, value_npk);
                break;
            case 3:
                cout << "Level-wise Display of BST:\n";
                levelwiseDisplay_npk(root_npk);
                break;
            case 4:
                cout << "Exiting program.\n";
                exit(0);
            default:
                cout << "Invalid choice. Please try again.\n";
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

--- Binary Search Tree Menu ---
1. Insert Node
2. Delete Node
3. Level-wise Display
4. Exit
Enter your choice: 1
Enter value to insert: 23

--- Binary Search Tree Menu ---
1. Insert Node
2. Delete Node
3. Level-wise Display
4. Exit
Enter your choice: 1
Enter value to insert: 22

--- Binary Search Tree Menu ---
1. Insert Node
2. Delete Node
3. Level-wise Display
4. Exit
Enter your choice: 1
Enter value to insert: 24

--- Binary Search Tree Menu ---
1. Insert Node
2. Delete Node
3. Level-wise Display
4. Exit
Enter your choice: 1
Enter value to insert: 25

--- Binary Search Tree Menu ---
1. Insert Node
2. Delete Node
3. Level-wise Display
4. Exit
Enter your choice: 1
Enter value to insert: 26

--- Binary Search Tree Menu ---
1. Insert Node
2. Delete Node
3. Level-wise Display
4. Exit
Enter your choice: 3
Level-wise Display of BST:
23
22 24
25
26

--- Binary Search Tree Menu ---
1. Insert Node
2. Delete Node
3. Level-wise Display
4. Exit
Enter your choice: 4
Exiting program.
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## CONCLUSION

<p>The program successfully implements a Binary Search Tree (BST) using dynamic memory allocation in C++.  
It supports insertion of new nodes, deletion of existing nodes (handling all three cases of deletion), and displays the structure level-wise using a queue for breadth-first traversal.  
This experiment helps understand hierarchical data storage and recursive programming concepts in trees.</p>

---


