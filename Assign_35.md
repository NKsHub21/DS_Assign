
# <center> ASSIGNMENT NO - 5 Unit_4 </center>

## Title :

**Create a Binary Tree and perform Recursive operations: Inorder, Preorder, Display Number of Leaf Nodes, Mirror Image.**

---

## AIM

<p>To implement recursive traversals, leaf counting, and mirroring for a binary tree.</p>

---

## OBJECTIVE

<p>Reinforce recursive definitions for traversal and structural operations on trees.</p>

---

## THEORY

<p>Recursive functions naturally process trees because each subtree is itself a tree. Inorder and preorder are straightforward, leaf counts accumulate base cases, and mirroring swaps child pointers recursively.</p>

---

## ALGORITHM

### Recursive Operations

1. Insert nodes level-wise using a queue.
2. Inorder Rec: L, Root, R.
3. Preorder Rec: Root, L, R.
4. Leaf count: if node is leaf return 1; else sum of children.
5. Mirror: swap children and recurse.

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

void inorderRec_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return;
    inorderRec_npk(root_npk->left_npk);
    cout << root_npk->data_npk << " ";
    inorderRec_npk(root_npk->right_npk);
}

void preorderRec_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return;
    cout << root_npk->data_npk << " ";
    preorderRec_npk(root_npk->left_npk);
    preorderRec_npk(root_npk->right_npk);
}

int leafCountRec_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return 0;
    if (root_npk->left_npk == NULL && root_npk->right_npk == NULL)
        return 1;
    return leafCountRec_npk(root_npk->left_npk) + leafCountRec_npk(root_npk->right_npk);
}

void mirrorRec_npk(Node_npk* root_npk) {
    if (root_npk == NULL)
        return;
    Node_npk* t_npk = root_npk->left_npk;
    root_npk->left_npk = root_npk->right_npk;
    root_npk->right_npk = t_npk;
    mirrorRec_npk(root_npk->left_npk);
    mirrorRec_npk(root_npk->right_npk);
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
            inorderRec_npk(root_npk);
            cout << endl;
        } else if (choice_npk == 3) {
            preorderRec_npk(root_npk);
            cout << endl;
        } else if (choice_npk == 4) {
            cout << "Leaf Nodes: " << leafCountRec_npk(root_npk) << endl;
        } else if (choice_npk == 5) {
            mirrorRec_npk(root_npk);
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

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 2
2 1 3 11 26 23

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 3
11 1 2 3 23 26

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 2
2 1 3 11 26 23

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 3
11 1 2 3 23 26

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
2 1 3 11 26 23

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 3
11 1 2 3 23 26

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 3
11 1 2 3 23 26

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 3
11 1 2 3 23 26

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
11 1 2 3 23 26

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 4
Leaf Nodes: 3

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 4
Leaf Nodes: 3

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Leaf Nodes: 3

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit

1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 5
Enter choice: 5


1. Insert  2. Inorder  3. Preorder  4. Leaf Count  5. Mirror  6. Exit
Enter choice: 6
PS C:\Users\Nandini\Documents\DS_VIT>

















```

---

## CONCLUSION

<p>Recursive traversal, counting, and mirroring reinforce essential tree recursion patterns and are concise to implement.</p>

---