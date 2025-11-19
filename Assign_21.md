

# Assignment: 1 Unit_3 Stack-Based Stock Price Tracker (Linked List Implementation)

<p>This document presents the implementation of a <code>StockPriceTracker_npk</code> program that uses a <b>Stack</b> built using a <b>Linked List</b>.  
It follows a strict C-style logic and naming convention for all functions and variables.</p>

---

##  Concept: Stack (Linked List) Structure

<p>The underlying data structure used here is a <b>Stack implemented using a Singly Linked List (SLL)</b>.  
Each node (<code>Node_npk</code>) stores an integer stock price (<code>price_npk</code>) and a pointer (<code>next_npk</code>) to the next node in the stack.</p>

| **Component** | **Description**                                        |
| :------------ | :----------------------------------------------------- |
| `Node_npk`    | Represents one stack element (a stock price record).   |
| `price_npk`   | The integer value representing the stock price.        |
| `next_npk`    | Pointer to the next node, linking all prices together. |

<p>The top of the stack always holds the <b>most recently entered stock price</b>.</p>

---

##  Algorithm: Stack Operations for Stock Tracking

<p>The program performs standard stack operations to maintain the stock price history.  
It uses a <b>Linked List</b> implementation to dynamically allocate memory, allowing unlimited price entries (bounded only by available memory).</p>

### **record_npk(price)**

<p>Adds a new stock price (push operation) to the stack.</p>

### **remove_npk()**

<p>Removes and returns the most recent stock price (pop operation).</p>

### **latest_npk()**

<p>Returns the top element (latest stock price) without removing it from the stack.</p>

### **isEmpty_npk()**

<p>Checks whether there are no recorded prices in the stack.</p>

### **isFull_npk()**

<p>Checks if memory allocation fails while creating a new node.</p>

---

##  C++ Code Implementation (Linked List Stack)

```cpp
#include <iostream>
using namespace std;

struct Node_npk {
    int price_npk;
    Node_npk* next_npk;
};

bool isEmpty_npk(Node_npk* head_npk) {
    return head_npk->next_npk == nullptr;
}

bool isFull_npk() {
    Node_npk* temp_npk = new(nothrow) Node_npk;
    if (temp_npk == nullptr)
        return true;
    delete temp_npk;
    return false;
}

bool record_npk(Node_npk* head_npk, int price_npk) {
    if (isFull_npk()) {
        cout << "Memory full. Cannot record price.\n";
        return false;
    }

    Node_npk* newNode_npk = new Node_npk;
    if (newNode_npk == nullptr) {
        cout << "Memory allocation failed.\n";
        return false;
    }

    newNode_npk->price_npk = price_npk;
    newNode_npk->next_npk = head_npk->next_npk;
    head_npk->next_npk = newNode_npk;
    return true;
}

bool remove_npk(Node_npk* head_npk, int &value_npk) {
    if (isEmpty_npk(head_npk)) {
        cout << "No prices recorded. Cannot remove.\n";
        return false;
    }

    Node_npk* temp_npk = head_npk->next_npk;
    value_npk = temp_npk->price_npk;
    head_npk->next_npk = temp_npk->next_npk;
    delete temp_npk;
    return true;
}

bool latest_npk(Node_npk* head_npk, int &value_npk) {
    if (isEmpty_npk(head_npk)) {
        cout << "No prices recorded.\n";
        return false;
    }

    value_npk = head_npk->next_npk->price_npk;
    return true;
}

void display_npk(Node_npk* head_npk) {
    if (isEmpty_npk(head_npk)) {
        cout << "No prices recorded.\n";
        return;
    }

    Node_npk* temp_npk = head_npk->next_npk;
    cout << "\nStock Price History (Latest → Oldest):\n";
    cout << "Top -> ";
    while (temp_npk != nullptr) {
        cout << "[" << temp_npk->price_npk << "] -> ";
        temp_npk = temp_npk->next_npk;
    }
    cout << "NULL\n";
}

int menu_npk() {
    int ch_npk;
    cout << "\n========== STOCK PRICE TRACKER ==========\n";
    cout << "1. Record new price\n";
    cout << "2. Remove latest price\n";
    cout << "3. View latest price\n";
    cout << "4. Show all recorded prices\n";
    cout << "5. Check if no prices are recorded\n";
    cout << "6. Exit\n";
    cout << "Enter your choice: ";
    cin >> ch_npk;
    return ch_npk;
}

int main_npk() {
    Node_npk* head_npk = new Node_npk;
    head_npk->next_npk = nullptr;

    int ch_npk, price_npk;

    while (true) {
        ch_npk = menu_npk();

        switch (ch_npk) {
            case 1:
                cout << "Enter stock price: ";
                cin >> price_npk;
                if (record_npk(head_npk, price_npk))
                    cout << "Price recorded successfully.\n";
                break;

            case 2:
                if (remove_npk(head_npk, price_npk))
                    cout << "Removed latest price: " << price_npk << endl;
                break;

            case 3:
                if (latest_npk(head_npk, price_npk))
                    cout << "Latest recorded price: " << price_npk << endl;
                break;

            case 4:
                display_npk(head_npk);
                break;

            case 5:
                if (isEmpty_npk(head_npk))
                    cout << "No prices recorded.\n";
                else
                    cout << "Prices are recorded.\n";
                break;

            case 6:
                cout << "Exiting program.\n";
                while (!isEmpty_npk(head_npk))
                    remove_npk(head_npk, price_npk);
                delete head_npk;
                return 0;

            default:
                cout << "Invalid choice. Please try again.\n";
        }
    }
    return 0;
}

// Entry point wrapper
int main() {
    return main_npk();
}
```

---

##  Algorithm Steps

### **Step 1:**

<p>Create a dummy head node (<code>head_npk</code>) to simplify insert and delete operations.</p>

### **Step 2:**

<p>Use <code>record_npk()</code> to push new stock prices to the top of the stack.</p>

### **Step 3:**

<p>Use <code>remove_npk()</code> to pop and remove the latest stock price.</p>

### **Step 4:**

<p>Use <code>latest_npk()</code> to check the latest recorded price without removing it.</p>

### **Step 5:**

<p>Display all stock prices using <code>display_npk()</code> to view history from latest to oldest.</p>

### **Step 6:**

<p>Before exiting, free all dynamically allocated memory.</p>

---

## 🧠 Concept Recap

<p>The <b>Stack</b> operates on the <b>LIFO (Last In, First Out)</b> principle.  
This implementation dynamically manages stock prices using linked list nodes, avoiding static size limitations.  
Each stack operation — <b>record</b>, <b>remove</b>, and <b>latest</b> — executes in constant time (O(1)).</p>

---

##  Output

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_21.cpp -o Assign_21 } ; if ($?) { .\Assign_21 }

========== STOCK PRICE TRACKER ==========
1. Record new price
2. Remove latest price
3. View latest price
4. Show all recorded prices
5. Check if no prices are recorded
6. Exit
Enter your choice: 3
No prices recorded.

========== STOCK PRICE TRACKER ==========
1. Record new price
2. Remove latest price
3. View latest price
4. Show all recorded prices
5. Check if no prices are recorded
6. Exit
Enter your choice: 1
Enter stock price: 100
Price recorded successfully.

========== STOCK PRICE TRACKER ==========
1. Record new price
2. Remove latest price
3. View latest price
4. Show all recorded prices
5. Check if no prices are recorded
6. Exit
Enter your choice: 5
There are recorded prices.

========== STOCK PRICE TRACKER ==========
1. Record new price
2. Remove latest price
3. View latest price
4. Show all recorded prices
5. Check if no prices are recorded
6. Exit
Enter your choice: 3
Latest recorded price: 100

========== STOCK PRICE TRACKER ==========
1. Record new price
2. Remove latest price
3. View latest price
4. Show all recorded prices
5. Check if no prices are recorded
6. Exit
Enter your choice: 6
6. Exit
Enter your choice: 3
Latest recorded price: 100

========== STOCK PRICE TRACKER ==========
1. Record new price
2. Remove latest price
3. View latest price
4. Show all recorded prices
5. Check if no prices are recorded
6. Exit
Enter your choice: 6

========== STOCK PRICE TRACKER ==========
1. Record new price
2. Remove latest price
3. View latest price
4. Show all recorded prices
5. Check if no prices are recorded
6. Exit
Enter your choice: 6
1. Record new price
2. Remove latest price
3. View latest price
4. Show all recorded prices
5. Check if no prices are recorded
6. Exit
Enter your choice: 6
4. Show all recorded prices
5. Check if no prices are recorded
6. Exit
Enter your choice: 6
5. Check if no prices are recorded
6. Exit
Enter your choice: 6
6. Exit
Enter your choice: 6
Enter your choice: 6
Exiting program.
PS C:\Users\Nandini\Documents\DS_VIT>









Exiting program.
PS C:\Users\Nandini\Documents\DS_VIT>








Exiting program.
PS C:\Users\Nandini\Documents\DS_VIT>






Exiting program.
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## 🧩 Conclusion

<p>The <b>Stock Price Tracker</b> efficiently maintains a record of stock prices using a <b>Stack implemented with a Linked List</b>.  
It dynamically adds, removes, and displays prices while maintaining LIFO behavior.  
This program demonstrates fundamental <b>stack operations</b>, <b>dynamic memory allocation</b>, and <b>menu-driven control</b> in C++.</p>

---

