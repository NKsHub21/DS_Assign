

# Assignment:   2 Unit_3  Infix to Postfix Conversion using Stack

<p>This document explains the implementation of an algorithm to convert an infix expression such as <code>a-b*c-d/e+f</code> into postfix form using a stack implemented through a linked list structure.</p>

---

## Concept: Infix and Postfix Expressions

<p>In an infix expression, operators appear between operands (for example, <code>A + B</code>).  
In a postfix expression (Reverse Polish Notation), operators are written after operands (for example, <code>A B +</code>).</p>

<p>The postfix notation removes the need for parentheses and uses a stack to handle operator precedence.</p>

---

## Stack Implementation Concept

<p>The stack is implemented using a singly linked list. Each node stores one operator or parenthesis.  
Operands (a, b, c, etc.) go directly to the output string, while operators are temporarily stored in the stack until they can be placed in the correct order.</p>

| Component       | Description                                             |
| :-------------- | :------------------------------------------------------ |
| `Node_npk`      | Represents a single stack element storing one operator. |
| `push_npk()`    | Adds an operator to the stack.                          |
| `pop_npk()`     | Removes and returns the top operator.                   |
| `peek_npk()`    | Checks the top operator without removing it.            |
| `isEmpty_npk()` | Returns true if the stack is empty.                     |

---

## Algorithm: Infix to Postfix Conversion

<p>1. If the symbol is an operand, append it directly to the output.  
2. If the symbol is an operator, pop operators from the stack that have higher or equal precedence and then push the current operator.  
3. If the symbol is '(', push it to the stack.  
4. If the symbol is ')', pop from the stack until '(' is found.  
5. After scanning the expression, pop all remaining operators to the output.</p>

---

## Step-by-Step Example

<p>Example Expression: <code>a - b * c - d / e + f</code></p>

| Token | Action                     | Stack (Bottom→Top) | Output                |
| :---: | :------------------------- | :----------------- | :-------------------- |
|   a   | Operand → output           | –                  | a                     |
|   -   | Push ‘-’                   | -                  | a                     |
|   b   | Operand → output           | -                  | a b                   |
|   *   | Push ‘*’                   | - *                | a b                   |
|   c   | Operand → output           | - *                | a b c                 |
|   -   | Pop ‘*’, Pop ‘-’, Push ‘-’ | -                  | a b c * -             |
|   d   | Operand → output           | -                  | a b c * - d           |
|   /   | Push ‘/’                   | - /                | a b c * - d           |
|   e   | Operand → output           | - /                | a b c * - d e         |
|   +   | Pop ‘/’, Pop ‘-’, Push ‘+’ | +                  | a b c * - d e / -     |
|   f   | Operand → output           | +                  | a b c * - d e / - f   |
|  End  | Pop ‘+’                    | –                  | a b c * - d e / - f + |

<p>Final Postfix Expression: <code>abc*-de/-f+</code></p>

---

## C++ Implementation

```cpp
#include <iostream>
#include <string>
using namespace std;

struct Node_npk {
    char op_npk;
    Node_npk* next_npk;
};

bool isEmpty_npk(Node_npk* head_npk) {
    return head_npk->next_npk == nullptr;
}

bool isFull_npk() {
    Node_npk* temp_npk = new(nothrow) Node_npk;
    if (!temp_npk) return true;
    delete temp_npk;
    return false;
}

bool push_npk(Node_npk* head_npk, char c_npk) {
    if (isFull_npk()) return false;
    Node_npk* newNode_npk = new Node_npk{c_npk, head_npk->next_npk};
    head_npk->next_npk = newNode_npk;
    return true;
}

bool pop_npk(Node_npk* head_npk, char &c_npk) {
    if (isEmpty_npk(head_npk)) return false;
    Node_npk* temp_npk = head_npk->next_npk;
    c_npk = temp_npk->op_npk;
    head_npk->next_npk = temp_npk->next_npk;
    delete temp_npk;
    return true;
}

bool peek_npk(Node_npk* head_npk, char &c_npk) {
    if (isEmpty_npk(head_npk)) return false;
    c_npk = head_npk->next_npk->op_npk;
    return true;
}

bool isOperand_npk(char ch_npk) {
    return ((ch_npk >= 'a' && ch_npk <= 'z') || (ch_npk >= 'A' && ch_npk <= 'Z') || (ch_npk >= '0' && ch_npk <= '9'));
}

int precedence_npk(char op_npk) {
    if (op_npk == '^') return 3;
    if (op_npk == '*' || op_npk == '/') return 2;
    if (op_npk == '+' || op_npk == '-') return 1;
    return 0;
}

bool isLeftAssociative_npk(char op_npk) {
    return (op_npk != '^');
}

string infixToPostfix_npk(const string &infix_npk) {
    Node_npk* head_npk = new Node_npk{'#', nullptr};
    string out_npk;
    for (char token_npk : infix_npk) {
        if (token_npk == ' ') continue;
        if (isOperand_npk(token_npk)) {
            out_npk.push_back(token_npk);
        } else if (token_npk == '(') {
            push_npk(head_npk, token_npk);
        } else if (token_npk == ')') {
            char top_npk;
            while (peek_npk(head_npk, top_npk) && top_npk != '(') {
                pop_npk(head_npk, top_npk);
                out_npk.push_back(top_npk);
            }
            if (peek_npk(head_npk, top_npk) && top_npk == '(')
                pop_npk(head_npk, top_npk);
        } else {
            char top_npk;
            while (!isEmpty_npk(head_npk) && peek_npk(head_npk, top_npk) && top_npk != '(' &&
                  (precedence_npk(top_npk) > precedence_npk(token_npk) ||
                  (precedence_npk(top_npk) == precedence_npk(token_npk) && isLeftAssociative_npk(token_npk)))) {
                pop_npk(head_npk, top_npk);
                out_npk.push_back(top_npk);
            }
            push_npk(head_npk, token_npk);
        }
    }
    char top_npk;
    while (pop_npk(head_npk, top_npk)) {
        if (top_npk != '(' && top_npk != ')')
            out_npk.push_back(top_npk);
    }
    delete head_npk;
    return out_npk;
}

int main_npk() {
    string expr_npk = "a-b*c-d/e+f";
    cout << "Infix   : " << expr_npk << "\n";
    string post_npk = infixToPostfix_npk(expr_npk);
    cout << "Postfix : " << post_npk << "\n";
    return 0;
}

int main() {
    return main_npk();
}
```

---

##  Output

```
cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
Infix   : a-b*c-d/e+f
Postfix : abc*-de/-f+
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## Conclusion

<p>The infix to postfix conversion uses a stack implemented with a singly linked list to handle operator precedence and associativity.  
Each operand is added directly to the output, while operators are managed through push and pop operations.  
For the given input expression <code>a-b*c-d/e+f</code>, the postfix expression generated is <code>abc*-de/-f+</code>.</p>

---
