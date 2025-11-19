# <center> ASSIGNMENT NO - 8 Unit_4</center>

## Title :

**Efficiently search a particular employee record using a tree data structure. Also sort the data on empid in ascending order.**

---

## AIM

<p>To implement a BST keyed by employee id for fast lookup and sorted listing.</p>

---

## OBJECTIVE

<p>Support insertion, search by id, and inorder traversal to view employees ordered by empid.</p>

---

## THEORY

<p>When employees are stored in a BST by id, search is logarithmic on average and inorder traversal yields ascending order, enabling both efficient retrieval and natural sorting.</p>

---

## ALGORITHM

### Employee BST

1. Insert `(empid, name, dept)` by `empid`.
2. Search for an id by traversing left or right.
3. Inorder traversal to print ascending ids.

---

## CODE

```cpp

#include <iostream>
#include <string>
#include <cstdlib>
using namespace std;

struct Emp_npk {
    int id_npk;
    string name_npk;
    string dept_npk;
    Emp_npk* left_npk;
    Emp_npk* right_npk;
};

Emp_npk* newEmp_npk(int id_npk, const string& name_npk, const string& dept_npk) {
    Emp_npk* t_npk = new Emp_npk;
    if (t_npk == NULL) {
        cout << "Memory allocation failed.\n";
        exit(1);
    }
    t_npk->id_npk = id_npk;
    t_npk->name_npk = name_npk;
    t_npk->dept_npk = dept_npk;
    t_npk->left_npk = NULL;
    t_npk->right_npk = NULL;
    return t_npk;
}

Emp_npk* insert_npk(Emp_npk* root_npk, int id_npk, const string& name_npk, const string& dept_npk) {
    if (root_npk == NULL)
        return newEmp_npk(id_npk, name_npk, dept_npk);
    if (id_npk < root_npk->id_npk)
        root_npk->left_npk = insert_npk(root_npk->left_npk, id_npk, name_npk, dept_npk);
    else if (id_npk > root_npk->id_npk)
        root_npk->right_npk = insert_npk(root_npk->right_npk, id_npk, name_npk, dept_npk);
    else
        cout << "Employee ID already exists.\n";
    return root_npk;
}

Emp_npk* search_npk(Emp_npk* root_npk, int id_npk) {
    while (root_npk != NULL) {
        if (id_npk == root_npk->id_npk)
            return root_npk;
        if (id_npk < root_npk->id_npk)
            root_npk = root_npk->left_npk;
        else
            root_npk = root_npk->right_npk;
    }
    return NULL;
}

void inorder_npk(Emp_npk* root_npk) {
    if (root_npk == NULL)
        return;
    inorder_npk(root_npk->left_npk);
    cout << "ID: " << root_npk->id_npk 
         << " | Name: " << root_npk->name_npk 
         << " | Department: " << root_npk->dept_npk << endl;
    inorder_npk(root_npk->right_npk);
}

int main_npk() {
    Emp_npk* root_npk = NULL;
    int choice_npk, id_npk;
    string name_npk, dept_npk;

    while (true) {
        cout << "\n--- Employee Binary Search Tree Menu ---\n";
        cout << "1. Insert Employee\n";
        cout << "2. Search Employee by ID\n";
        cout << "3. Display Employees (Ascending Order)\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice_npk;

        if (choice_npk == 1) {
            cout << "Enter Employee ID: ";
            cin >> id_npk;
            cin.ignore(); // clear buffer before getline
            cout << "Enter Employee Name: ";
            getline(cin, name_npk);
            cout << "Enter Department: ";
            getline(cin, dept_npk);
            root_npk = insert_npk(root_npk, id_npk, name_npk, dept_npk);
        } 
        else if (choice_npk == 2) {
            cout << "Enter Employee ID to search: ";
            cin >> id_npk;
            Emp_npk* f_npk = search_npk(root_npk, id_npk);
            if (f_npk)
                cout << "Employee Found:\nID: " << f_npk->id_npk 
                     << " | Name: " << f_npk->name_npk 
                     << " | Department: " << f_npk->dept_npk << endl;
            else
                cout << "Employee Not Found.\n";
        } 
        else if (choice_npk == 3) {
            cout << "\n--- Employee List (Ascending Order by ID) ---\n";
            inorder_npk(root_npk);
        } 
        else if (choice_npk == 4) {
            cout << "Exiting...\n";
            break;
        } 
        else {
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
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }

--- Employee Binary Search Tree Menu ---
1. Insert Employee
2. Search Employee by ID
3. Display Employees (Ascending Order)
4. Exit
Enter your choice: 1  
Enter Employee ID: 1
Enter Employee Name: Krish
Enter Department: IT

--- Employee Binary Search Tree Menu ---
1. Insert Employee
2. Search Employee by ID
3. Display Employees (Ascending Order)
4. Exit
Enter your choice: 1
Enter Employee ID: 2
Enter Employee Name: Lavanya
Enter Department: HR

--- Employee Binary Search Tree Menu ---
1. Insert Employee
2. Search Employee by ID
3. Display Employees (Ascending Order)
4. Exit
Enter your choice: 1
Enter Employee ID: 6
Enter Employee Name: Ojas
Enter Department: Marketing

--- Employee Binary Search Tree Menu ---
1. Insert Employee
2. Search Employee by ID
3. Display Employees (Ascending Order)
4. Exit
Enter your choice: 1
Enter Employee ID: 4
Enter Employee Name: Tejas
Enter Department: Sales

--- Employee Binary Search Tree Menu ---
1. Insert Employee
2. Search Employee by ID
3. Display Employees (Ascending Order)
4. Exit
Enter your choice: 3

--- Employee List (Ascending Order by ID) ---
ID: 1 | Name: Krish | Department: IT
ID: 2 | Name: Lavanya | Department: HR
ID: 4 | Name: Tejas | Department: Sales
ID: 6 | Name: Ojas | Department: Marketing

--- Employee Binary Search Tree Menu ---
1. Insert Employee
2. Search Employee by ID
3. Display Employees (Ascending Order)
4. Exit
Enter your choice: 4
Exiting...
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## CONCLUSION

<p>Employee records were efficiently stored and retrieved using a BST keyed by empid, and sorted listing was obtained through inorder traversal.</p>

---