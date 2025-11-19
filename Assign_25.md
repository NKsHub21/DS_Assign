

# <center> ASSIGNMENT NO - 5 Unit_3 </center>

## Title :

Write a program to evaluate a postfix expression (Reverse Polish Notation) consisting of single-digit operands and binary operators (+, -, *, /) using stack implemented with an array.

---

## AIM

<p>To write a C program that evaluates a postfix expression using a stack implemented with an array and returns the computed result.</p>

---

## OBJECTIVE

<p>The objective of this assignment is to understand how the stack data structure can be used to evaluate arithmetic expressions written in postfix (Reverse Polish) notation.  
The program demonstrates stack-based operand storage and evaluation through the use of push and pop operations.</p>

---

## What is Postfix Expression Evaluation?

<p>In a postfix expression (Reverse Polish Notation), the operator appears after the operands.  
For example, the infix expression <code>(2 + 3) * 4</code> is represented in postfix as <code>2 3 + 4 *</code>.  
To evaluate a postfix expression, we use a stack to store operands and apply operators as they appear.</p>

---

## Algorithm

### Algorithm to Evaluate a Postfix Expression

```
1. Start
2. Initialize an empty stack (array of integers)
3. For each symbol in the postfix expression:
      a. If the symbol is an operand (0–9):
             Push it onto the stack
      b. If the symbol is an operator (+, -, *, /):
             Pop the top two elements from the stack
             Apply the operator in correct order:
                 operand2 <operator> operand1
             Push the result back onto the stack
4. After scanning the entire expression:
      The final result will be the only element remaining in the stack
5. Display the result
6. End
```

---

## Code

```
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>

#define SIZE 50

int stack_npk[SIZE];
int top_npk = -1;

int isFull_npk() {
    return (top_npk == SIZE - 1);
}

int isEmpty_npk() {
    return (top_npk == -1);
}

void push_npk(int val_npk) {
    if (isFull_npk()) {
        printf("Stack Overflow\n");
        exit(1);
    }
    top_npk++;
    stack_npk[top_npk] = val_npk;
}

int pop_npk() {
    if (isEmpty_npk()) {
        printf("Stack Underflow\n");
        exit(1);
    }
    int val_npk = stack_npk[top_npk];
    top_npk--;
    return val_npk;
}

int evaluatePostfix_npk(char exp_npk[]) {
    for (int i = 0; exp_npk[i] != '\0'; i++) {
        char ch_npk = exp_npk[i];

        if (isdigit(ch_npk)) {
            push_npk(ch_npk - '0');
        } 
        else if (ch_npk == '+' || ch_npk == '-' || ch_npk == '*' || ch_npk == '/') {
            int val1_npk = pop_npk();
            int val2_npk = pop_npk();

            switch (ch_npk) {
                case '+': push_npk(val2_npk + val1_npk); break;
                case '-': push_npk(val2_npk - val1_npk); break;
                case '*': push_npk(val2_npk * val1_npk); break;
                case '/': push_npk(val2_npk / val1_npk); break;
            }
        }
    }
    return pop_npk();
}

int main_npk() {
    char exp_npk[SIZE];
    printf("Enter a postfix expression: ");
    scanf("%s", exp_npk);

    int result_npk = evaluatePostfix_npk(exp_npk);
    printf("The result of postfix evaluation is: %d\n", result_npk);

    return 0;
}

int main() {
    return main_npk();
}
```

---

## Output

```
cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_25.cpp -o Assign_25 } ; if ($?) { .\Assign_25 }
Enter a postfix expression: 23+4*
The result of postfix evaluation is: 20
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## Conclusion

<p>The program successfully evaluates postfix (Reverse Polish) expressions using a stack implemented through an array.  
Each operand is pushed onto the stack, and when an operator is encountered, the top two operands are popped, the operation is performed, and the result is pushed back onto the stack.  
The final result obtained from the stack represents the evaluated value of the postfix expression.</p>

---
