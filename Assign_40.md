# <center> ASSIGNMENT NO - 10 Unit_4 </center>

## Title :

**Implement deletion operations in the product inventory system using a search tree: Delete by product code and delete all expired products based on current date.**

---

## AIM

<p>To support targeted deletion by unique product code and bulk deletion of expired products in a name-ordered BST.</p>

---

## OBJECTIVE

<p>Locate nodes by code using a traversal, delete by name key in the name-ordered tree, and remove all expired items relative to the current date.</p>

---

## THEORY

<p>When the tree is keyed by product name, deletion by code requires a search pass to identify the name associated with a given code, then deletion by that name. Bulk deletion of expired products proceeds by collecting all expired nodes first to avoid mutation during traversal, then deleting them one by one.</p>

---

## ALGORITHM

### Deletion by Code / Delete All Expired

1. Insert by product name.
2. To delete by code: traverse and collect the product name(s) matching the code, then delete by name.
3. To delete expired: traverse and collect all names with `exp < current`, then delete each by name.
4. Display to verify.

---

## CODE

```cpp
#include <iostream>
#include <string>
#include <vector>
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

Prod_npk* minNode_npk(Prod_npk* root_npk) {
    while (root_npk && root_npk->left_npk)
        root_npk = root_npk->left_npk;
    return root_npk;
}

Prod_npk* deleteByName_npk(Prod_npk* root_npk, const string& n_npk) {
    if (root_npk == NULL)
        return root_npk;
    if (n_npk < root_npk->name_npk)
        root_npk->left_npk = deleteByName_npk(root_npk->left_npk, n_npk);
    else if (n_npk > root_npk->name_npk)
        root_npk->right_npk = deleteByName_npk(root_npk->right_npk, n_npk);
    else {
        if (root_npk->left_npk == NULL) {
            Prod_npk* t_npk = root_npk->right_npk;
            delete root_npk;
            return t_npk;
        } else if (root_npk->right_npk == NULL) {
            Prod_npk* t_npk = root_npk->left_npk;
            delete root_npk;
            return t_npk;
        } else {
            Prod_npk* t_npk = minNode_npk(root_npk->right_npk);
            root_npk->name_npk = t_npk->name_npk;
            root_npk->code_npk = t_npk->code_npk;
            root_npk->price_npk = t_npk->price_npk;
            root_npk->qty_npk = t_npk->qty_npk;
            root_npk->recv_npk = t_npk->recv_npk;
            root_npk->exp_npk = t_npk->exp_npk;
            root_npk->right_npk = deleteByName_npk(root_npk->right_npk, t_npk->name_npk);
        }
    }
    return root_npk;
}

bool expired_npk(const string& cur_npk, const string& e_npk) {
    return e_npk < cur_npk;
}

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

void collectByCode_npk(Prod_npk* root_npk, const string& code_npk, vector<string>& names_npk) {
    if (root_npk == NULL)
        return;
    if (root_npk->code_npk == code_npk)
        names_npk.push_back(root_npk->name_npk);
    collectByCode_npk(root_npk->left_npk, code_npk, names_npk);
    collectByCode_npk(root_npk->right_npk, code_npk, names_npk);
}

void collectExpiredNames_npk(Prod_npk* root_npk, const string& cur_npk, vector<string>& names_npk) {
    if (root_npk == NULL)
        return;
    if (expired_npk(cur_npk, root_npk->exp_npk))
        names_npk.push_back(root_npk->name_npk);
    collectExpiredNames_npk(root_npk->left_npk, cur_npk, names_npk);
    collectExpiredNames_npk(root_npk->right_npk, cur_npk, names_npk);
}

int main_npk() {
    Prod_npk* root_npk = NULL;
    int choice_npk, qty_npk;
    string code_npk, name_npk, recv_npk, exp_npk, cur_npk;
    double price_npk;

    while (true) {
        cout << "\n===== PRODUCT MANAGEMENT MENU =====\n";
        cout << "1. Insert Product\n";
        cout << "2. Display All Products (Inorder)\n";
        cout << "3. Delete Products by Code\n";
        cout << "4. Delete All Expired Products\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice_npk;

        if (choice_npk == 1) {
            cin.ignore();
            cout << "Enter Product Code: ";
            getline(cin, code_npk);
            cout << "Enter Product Name: ";
            getline(cin, name_npk);
            cout << "Enter Price: ";
            cin >> price_npk;
            cout << "Enter Quantity: ";
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
                cout << "No products available.\n";
            else {
                cout << "\n--- Product List (Inorder Traversal) ---\n";
                inorder_npk(root_npk);
            }
        } 
        else if (choice_npk == 3) {
            if (root_npk == NULL) {
                cout << "No products to delete.\n";
                continue;
            }
            cin.ignore();
            cout << "Enter Product Code to delete: ";
            getline(cin, code_npk);
            vector<string> names_npk;
            collectByCode_npk(root_npk, code_npk, names_npk);
            if (names_npk.empty())
                cout << "No product found with this code.\n";
            else {
                for (const auto& name : names_npk)
                    root_npk = deleteByName_npk(root_npk, name);
                cout << "Deleted all products with code: " << code_npk << endl;
            }
        } 
        else if (choice_npk == 4) {
            if (root_npk == NULL) {
                cout << "No products available.\n";
                continue;
            }
            cin.ignore();
            cout << "Enter Current Date (YYYY-MM-DD): ";
            getline(cin, cur_npk);
            vector<string> names_npk;
            collectExpiredNames_npk(root_npk, cur_npk, names_npk);
            if (names_npk.empty())
                cout << "No expired products found.\n";
            else {
                for (const auto& name : names_npk)
                    root_npk = deleteByName_npk(root_npk, name);
                cout << "Deleted all expired products.\n";
            }
        } 
        else if (choice_npk == 5) {
            cout << "Exiting...\n";
            break;
        } 
        else {
            cout << "Invalid choice! Please try again.\n";
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

===== PRODUCT MANAGEMENT MENU =====
1. Insert Product
2. Display All Products (Inorder)
3. Delete Products by Code
4. Delete All Expired Products
5. Exit
Enter your choice: 1
Enter Product Code: 123
Enter Product Name: Pan
Enter Price: 1000
Enter Quantity: 4
Enter Received Date (YYYY-MM-DD): 2025-05-21
Enter Expiry Date (YYYY-MM-DD): 20205-06-22

===== PRODUCT MANAGEMENT MENU =====
1. Insert Product
2. Display All Products (Inorder)
3. Delete Products by Code
4. Delete All Expired Products
5. Exit
Enter your choice: 2

--- Product List (Inorder Traversal) ---
Name: Pan | Code: 123 | Price: 1000 | Qty: 4 | Received: 2025-05-21 | Expiry: 20205-06-22

===== PRODUCT MANAGEMENT MENU =====
1. Insert Product
2. Display All Products (Inorder)
3. Delete Products by Code
4. Delete All Expired Products
5. Exit
Enter your choice: 3
Enter Product Code to delete: 123
Deleted all products with code: 123

===== PRODUCT MANAGEMENT MENU =====
1. Insert Product
2. Display All Products (Inorder)
3. Delete Products by Code
4. Delete All Expired Products
5. Exit
Enter your choice: 4
No products available.

===== PRODUCT MANAGEMENT MENU =====
1. Insert Product
2. Display All Products (Inorder)
3. Delete Products by Code
4. Delete All Expired Products
5. Exit
Enter your choice:
```

---

## CONCLUSION

<p>Deletion by code and bulk deletion of expired products were implemented by collecting matching names and then removing by name in the name-ordered BST, ensuring correctness and stability during structural updates.</p>

---