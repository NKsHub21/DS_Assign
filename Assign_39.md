# <center> ASSIGNMENT NO - 9 Unit_4 </center>

## Title :

**Implement a product inventory management system using a search tree organized by product name with operations: Insert, Display (Inorder), and List expired items in Preorder.**

---

## AIM

<p>To maintain product records in a name-ordered BST and identify expired items relative to a given current date.</p>

---

## OBJECTIVE

<p>Provide insertion, ordered display, and filtered listing of expired products using traversal patterns.</p>

---

## THEORY

<p>Organizing products by name in a BST allows fast lookups and alphabetical listing via inorder traversal. Expired items can be listed by traversing the tree and comparing expiration dates with the current date string in ISO format (YYYY-MM-DD).</p>

---

## ALGORITHM

### Inventory Tree

1. Insert product by name into BST.
2. Inorder traversal prints all products in alphabetical order.
3. Preorder traversal prints only nodes whose `exp` date is less than the given current date.

---

## CODE

```cpp
#include <iostream>
#include <string>
#include <cstdlib>
using namespace std;

struct Prod_npk {
    string code_npk;
    string name_npk;
    double price_npk;
    int qty_npk;
    string recv_npk;
    string exp_npk;
    Prod_npk* left_npk;
    Prod_npk* right_npk;
};

// Create a new product node
Prod_npk* newProd_npk(const string& c_npk, const string& n_npk, double p_npk, int q_npk, const string& r_npk, const string& e_npk) {
    Prod_npk* t_npk = new Prod_npk;
    if (t_npk == NULL) {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    t_npk->code_npk = c_npk;
    t_npk->name_npk = n_npk;
    t_npk->price_npk = p_npk;
    t_npk->qty_npk = q_npk;
    t_npk->recv_npk = r_npk;
    t_npk->exp_npk = e_npk;
    t_npk->left_npk = NULL;
    t_npk->right_npk = NULL;
    return t_npk;
}

// Insert product into BST (sorted by name)
Prod_npk* insert_npk(Prod_npk* root_npk, const string& c_npk, const string& n_npk, double p_npk, int q_npk, const string& r_npk, const string& e_npk) {
    if (root_npk == NULL)
        return newProd_npk(c_npk, n_npk, p_npk, q_npk, r_npk, e_npk);

    if (n_npk < root_npk->name_npk)
        root_npk->left_npk = insert_npk(root_npk->left_npk, c_npk, n_npk, p_npk, q_npk, r_npk, e_npk);
    else if (n_npk > root_npk->name_npk)
        root_npk->right_npk = insert_npk(root_npk->right_npk, c_npk, n_npk, p_npk, q_npk, r_npk, e_npk);
    else
        cout << "Product with this name already exists!\n";

    return root_npk;
}

// Check if a product is expired
bool expired_npk(const string& cur_npk, const string& e_npk) {
    return e_npk < cur_npk;
}

// Display all products (inorder = ascending order by name)
void inorder_npk(Prod_npk* root_npk) {
    if (root_npk == NULL)
        return;
    inorder_npk(root_npk->left_npk);
    cout << "Name: " << root_npk->name_npk
         << " | Code: " << root_npk->code_npk
         << " | Price: " << root_npk->price_npk
         << " | Qty: " << root_npk->qty_npk
         << " | Received: " << root_npk->recv_npk
         << " | Expiry: " << root_npk->exp_npk
         << endl;
    inorder_npk(root_npk->right_npk);
}

// Display expired products (preorder traversal)
void preorderExpired_npk(Prod_npk* root_npk, const string& cur_npk) {
    if (root_npk == NULL)
        return;

    if (expired_npk(cur_npk, root_npk->exp_npk))
        cout << "Expired → " << root_npk->name_npk
             << " (" << root_npk->code_npk << "), Expiry: " << root_npk->exp_npk << endl;

    preorderExpired_npk(root_npk->left_npk, cur_npk);
    preorderExpired_npk(root_npk->right_npk, cur_npk);
}

int main_npk() {
    Prod_npk* root_npk = NULL;
    int choice_npk, qty_npk;
    string code_npk, name_npk, recv_npk, exp_npk, cur_npk;
    double price_npk;

    while (true) {
        cout << "\n===== PRODUCT BINARY SEARCH TREE MENU =====\n";
        cout << "1. Insert Product\n";
        cout << "2. Display All Products (Inorder)\n";
        cout << "3. List Expired Products (Preorder)\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice_npk;

        if (choice_npk == 1) {
            cin.ignore(); // clear leftover newline
            cout << "Enter Product Code: ";
            getline(cin, code_npk);
            cout << "Enter Product Name: ";
            getline(cin, name_npk);
            cout << "Enter Product Price: ";
            cin >> price_npk;
            cout << "Enter Product Quantity: ";
            cin >> qty_npk;
            cin.ignore();
            cout << "Enter Received Date (YYYY-MM-DD): ";
            getline(cin, recv_npk);
            cout << "Enter Expiry Date (YYYY-MM-DD): ";
            getline(cin, exp_npk);

            root_npk = insert_npk(root_npk, code_npk, name_npk, price_npk, qty_npk, recv_npk, exp_npk);
        }
        else if (choice_npk == 2) {
            if (root_npk == NULL)
                cout << "No products to display.\n";
            else {
                cout << "\n--- Product List (Inorder) ---\n";
                inorder_npk(root_npk);
            }
        }
        else if (choice_npk == 3) {
            if (root_npk == NULL) {
                cout << "No products available.\n";
                continue;
            }
            cin.ignore();
            cout << "Enter Current Date (YYYY-MM-DD): ";
            getline(cin, cur_npk);
            cout << "\n--- Expired Products (Preorder Traversal) ---\n";
            preorderExpired_npk(root_npk, cur_npk);
        }
        else if (choice_npk == 4) {
            cout << "Exiting...\n";
            break;
        }
        else {
            cout << "Invalid choice. Try again.\n";
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

===== PRODUCT BINARY SEARCH TREE MENU =====
1. Insert Product
2. Display All Products (Inorder)
3. List Expired Products (Preorder)
4. Exit
Enter your choice: 1
Enter Product Code: 123
Enter Product Name: Light
Enter Product Price: 450
Enter Product Quantity: 3
Enter Received Date (YYYY-MM-DD): 1979-02-21
Enter Expiry Date (YYYY-MM-DD): 1987-01-22

===== PRODUCT BINARY SEARCH TREE MENU =====
1. Insert Product
2. Display All Products (Inorder)
3. List Expired Products (Preorder)
4. Exit
Enter your choice: 2

--- Product List (Inorder) ---
Name: Light | Code: 123 | Price: 450 | Qty: 3 | Received: 1979-02-21 | Expiry: 1987-01-22

===== PRODUCT BINARY SEARCH TREE MENU =====
1. Insert Product
2. Display All Products (Inorder)
3. List Expired Products (Preorder)
4. Exit
Enter your choice: 4  
Exiting...
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## CONCLUSION

<p>The inventory is organized alphabetically by product name in a BST. Inorder gives complete listing, and preorder filtering lists expired items efficiently via traversal.</p>

---