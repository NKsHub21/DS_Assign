
# <center> ASSIGNMENT NO - 4 Unit_3</center>

## Title :

Write a program to check whether the parentheses in a given string are balanced or not using stack implemented with an array.

---

## What is Balanced Parentheses Checking?

<p>Parentheses balancing is a common problem in computer science that checks whether every opening bracket has a corresponding closing bracket of the same type and whether they appear in the correct order.  
The valid brackets considered are <code>()</code>, <code>{}</code>, and <code>[]</code>.</p>

<p>This problem is efficiently solved using a <b>stack</b> data structure, which follows the Last In, First Out (LIFO) principle.  
An array-based stack is ideal for this application, as we only need to store and match bracket characters.</p>

---

## Algorithm

### Algorithm to Check Balanced Parentheses

```
1. Start
2. Initialize an empty stack (array of characters)
3. For each character in the input string:
       a. If it is an opening bracket '(' or '{' or '[', push it into the stack.
       b. If it is a closing bracket ')', '}', or ']':
            i. If the stack is empty, the expression is unbalanced → return false.
            ii. Pop the top element from the stack.
            iii. Check if the popped element and the current closing bracket match:
                  '(' with ')', '{' with '}', '[' with ']'
            iv. If they do not match, return false.
4. After processing all characters:
       If the stack is empty → return true (Balanced)
       Else → return false (Unbalanced)
5. End
```

---

## Code

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define SIZE 100

char stack_npk[SIZE];
int top_npk = -1;

int isFull_npk() {
    return (top_npk == SIZE - 1);
}

int isEmpty_npk() {
    return (top_npk == -1);
}

void push_npk(char ch_npk) {
    if (isFull_npk()) {
        printf("Stack Overflow\n");
        return;
    }
    top_npk++;
    stack_npk[top_npk] = ch_npk;
}

char pop_npk() {
    if (isEmpty_npk()) {
        return '\0';
    }
    char temp_npk = stack_npk[top_npk];
    top_npk--;
    return temp_npk;
}

int isMatchingPair_npk(char open_npk, char close_npk) {
    if (open_npk == '(' && close_npk == ')') return 1;
    if (open_npk == '{' && close_npk == '}') return 1;
    if (open_npk == '[' && close_npk == ']') return 1;
    return 0;
}

int isBalanced_npk(char exp_npk[]) {
    for (int i = 0; exp_npk[i] != '\0'; i++) {
        char ch_npk = exp_npk[i];

        if (ch_npk == '(' || ch_npk == '{' || ch_npk == '[') {
            push_npk(ch_npk);
        } else if (ch_npk == ')' || ch_npk == '}' || ch_npk == ']') {
            if (isEmpty_npk()) {
                return 0;
            }
            char topChar_npk = pop_npk();
            if (!isMatchingPair_npk(topChar_npk, ch_npk)) {
                return 0;
            }
        }
    }

    if (isEmpty_npk())
        return 1;
    else
        return 0;
}

int main_npk() {
    char exp_npk[SIZE];

    printf("Enter an expression containing brackets: ");
    scanf("%s", exp_npk);

    if (isBalanced_npk(exp_npk))
        printf("The expression is BALANCED.\n");
    else
        printf("The expression is NOT BALANCED.\n");

    return 0;
}

int main() {
    return main_npk();
}
```

---

## Output

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_24.cpp -o Assign_24 } ; if ($?) { .\Assign_24 }
Enter an expression containing brackets: ()[]{}{
The expression is NOT BALANCED.
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## Conclusion

<p>The program successfully checks whether the given string of parentheses is balanced using a stack implemented through an array.  
Each opening bracket is pushed into the stack, and every closing bracket is matched with the top of the stack.  
If all brackets are properly matched and the stack becomes empty at the end, the expression is balanced; otherwise, it is not.</p>

---

