`Unit-IV_Assignment_4_BinaryTree_Nonrecursive_Traversals_Leaf_Mirror.md`

# <center> ASSIGNMENT NO - 4 Unit_4</center>

## Title :

**Create a Binary Tree and perform Nonrecursive operations: Inorder, Preorder, Display Number of Leaf Nodes, Mirror Image.**

---

## AIM

<p>To build a general binary tree and implement iterative traversals, compute the number of leaves, and mirror the tree without recursion.</p>

---

## OBJECTIVE

<p>Develop proficiency with stacks and queues to traverse and modify trees iteratively.</p>

---

## THEORY

<p>Nonrecursive traversals simulate recursion through explicit stacks and queues. Inorder and preorder can be implemented using a stack, leaf counting via BFS with a queue, and mirroring by swapping children during BFS traversal.</p>

---

## ALGORITHM

### Nonrecursive Operations

1. Insert nodes level-wise using a queue.
2. Inorder (iterative): simulate recursion using a stack.
3. Preorder (iterative): push right then left to stack.
4. Leaf count: BFS and count nodes with both children null.
5. Mirror: BFS and swap left and right at each node.

---

## CODE

```cpp
#include <iostream>
#include <queue>
#include <stack>
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

Node_npk* insertLevel_npk(Node_npk* root_npk, int value_npk) {
    Node_npk* n_npk = newNode_npk(value_npk);
    if (root_npk == NULL)
        return n_npk;
    queue<Node_npk*> q_npk;
    q_npk.push(root_npk);
    while (!q_npk.empty()) {
        Node_npk* cur_npk = q_npk.front();
        q_npk.pop();
        if (cur_npk->left_npk == NULL) {
            cur_npk->left_npk = n_npk;
            break;
        } else {
            q_npk.push(cur_npk->left_npk);
        }
        if (cur_npk->right_npk == NULL) {
            cur_npk->right_npk = n_npk;
            break;
        } else {
            q_npk.push(cur_npk->right_npk);
        }
    }
    return root_npk;
}

void inorderIter_npk(Node_npk* root_npk) {
    stack<Node_npk*> st_npk;
    Node_npk* cur_npk = root_npk;
    while (cur_npk != NULL || !st_npk.empty()) {
        while (cur_npk != NULL) {
            st_npk.push(cur_npk);
            cur_npk = cur_npk->left_npk;
        }
        cur_npk = st_npk.top();
        st_npk.pop();
        cout << cur_npk->data_npk << " ";
        cur_npk = cur_npk->right_npk;
    }
    cout << endl;
}

void preorderIter_npk(Node_npk* root_npk) {
    if (root_npk == NULL) {
        cout << endl;
        return;
    }
    stack<Node_npk*> st_npk;
    st_npk.push(root_npk);
    while (!st_npk.empty()) {
        Node_npk* cur_npk = st_npk.top();
        st_npk.pop();
        cout << cur_npk->data_npk << " ";
        if (cur_npk->right_npk)
            st_npk.push(cur_npk->right_npk);
        if (cur_npk->left_npk)
            st_npk.push(cur_npk->left_npk);
    }
    cout << endl;
}

int leafCountIter_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return 0;
    int c_npk = 0;
    queue<Node_npk*> q_npk;
    q_npk.push(root_npk);
    while (!q_npk.empty()) {
        Node_npk* cur_npk = q_npk.front();
        q_npk.pop();
        if (cur_npk->left_npk == NULL && cur_npk->right_npk == NULL)
            c_npk++;
        if (cur_npk->left_npk)
            q_npk.push(cur_npk->left_npk);
        if (cur_npk->right_npk)
            q_npk.push(cur_npk->right_npk);
    }
    return c_npk;
}

void mirrorIter_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return;
    queue<Node_npk*> q_npk;
    q_npk.push(root_npk);
    while (!q_npk.empty()) {
        Node_npk* cur_npk = q_npk.front();
        q_npk.pop();
        Node_npk* t_npk = cur_npk->left_npk;
        cur_npk->left_npk = cur_npk->right_npk;
        cur_npk->right_npk = t_npk;
        if (cur_npk->left_npk)
            q_npk.push(cur_npk->left_npk);
        if (cur_npk->right_npk)
            q_npk.push(cur_npk->right_npk);
    }
}

int main_npk() {
    Node_npk* root_npk = NULL;
    int choice_npk, value_npk;
    while (true) {
        cout << "\n1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit\n";
        cout << "Enter choice: ";
        cin >> choice_npk;
        if (choice_npk == 1) {
            cin >> value_npk;
            root_npk = insertLevel_npk(root_npk, value_npk);
        } else if (choice_npk == 2) {
            inorderIter_npk(root_npk);
        } else if (choice_npk == 3) {
            preorderIter_npk(root_npk);
        } else if (choice_npk == 4) {
            cout << "Leaf Nodes: " << leafCountIter_npk(root_npk) << endl;
        } else if (choice_npk == 5) {
            mirrorIter_npk(root_npk);
        } else if (choice_npk == 6) {
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
cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 1
11

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 1
1

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 1
23

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 1
2

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 1
3

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 1
26

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 2
2 1 3 11 26 23 

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 3
11 1 2 3 23 26 

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 4
Leaf Nodes: 3

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 5

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 6
PS C:\Users\Nandini\Documents\DS_VIT> 
```

---

## CONCLUSION

<p>Iterative traversals and transforms were implemented using stacks and queues, demonstrating nonrecursive strategies for binary tree manipulation.</p>

---