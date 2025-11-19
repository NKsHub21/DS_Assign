

# <center> ASSIGNMENT NO - 3 Unit_3 </center>

## Title :

Implement multiple stacks (two stacks) using a single array and perform the operations Push, Pop, Stack Overflow, Stack Underflow, and Display.

---

## What is Multiple Stack Implementation Using Array?

<p>A multiple stack implementation allows two or more stacks to coexist in a single array.  
Instead of creating separate arrays for each stack, a shared memory structure is used to optimize space.  
In this implementation, two stacks are created inside one array:</p>

<ul>
<li><b>Stack 1</b> grows from the left end (index 0) towards the right.</li>
<li><b>Stack 2</b> grows from the right end (index SIZE-1) towards the left.</li>
</ul>

<p>When both stacks meet, a <b>Stack Overflow</b> condition occurs.  
This approach efficiently uses available memory space and demonstrates how two independent stacks can be maintained in one array.</p>

---

## Algorithm

### 1. Push Operation

```
1. Start
2. Check if array is full using the condition (top1 + 1 == top2)
3. If full, display "Stack Overflow"
4. Else if pushing into Stack 1
      Increment top1
      Insert value into stack[top1]
   Else if pushing into Stack 2
      Decrement top2
      Insert value into stack[top2]
5. End
```

### 2. Pop Operation

```
1. Start
2. If popping from Stack 1
      Check if top1 == -1 → "Stack Underflow"
      Else display stack[top1] and decrement top1
3. If popping from Stack 2
      Check if top2 == SIZE → "Stack Underflow"
      Else display stack[top2] and increment top2
4. End
```

### 3. Display Operation

```
1. Start
2. If displaying Stack 1
      If top1 == -1 → "Stack 1 Empty"
      Else print elements from top1 down to 0
3. If displaying Stack 2
      If top2 == SIZE → "Stack 2 Empty"
      Else print elements from top2 up to SIZE-1
4. End
```

---

## Code

```
#include <stdio.h>
#include <stdlib.h>

#define SIZE 10

int stack_npk[SIZE];
int top1_npk = -1;
int top2_npk = SIZE;

int isFull_npk() {
    return (top1_npk + 1 == top2_npk);
}

int isEmpty1_npk() {
    return (top1_npk == -1);
}

int isEmpty2_npk() {
    return (top2_npk == SIZE);
}

void push1_npk(int value_npk) {
    if (isFull_npk()) {
        printf("Stack Overflow! Cannot push %d in Stack 1.\n", value_npk);
        return;
    }
    top1_npk++;
    stack_npk[top1_npk] = value_npk;
    printf("%d pushed to Stack 1.\n", value_npk);
}

void push2_npk(int value_npk) {
    if (isFull_npk()) {
        printf("Stack Overflow! Cannot push %d in Stack 2.\n", value_npk);
        return;
    }
    top2_npk--;
    stack_npk[top2_npk] = value_npk;
    printf("%d pushed to Stack 2.\n", value_npk);
}

void pop1_npk() {
    if (isEmpty1_npk()) {
        printf("Stack Underflow! Stack 1 is empty.\n");
        return;
    }
    printf("Popped %d from Stack 1.\n", stack_npk[top1_npk]);
    top1_npk--;
}

void pop2_npk() {
    if (isEmpty2_npk()) {
        printf("Stack Underflow! Stack 2 is empty.\n");
        return;
    }
    printf("Popped %d from Stack 2.\n", stack_npk[top2_npk]);
    top2_npk++;
}

void display1_npk() {
    if (isEmpty1_npk()) {
        printf("Stack 1 is empty.\n");
        return;
    }
    printf("Stack 1 elements (top to bottom):\n");
    for (int i = top1_npk; i >= 0; i--)
        printf("%d\n", stack_npk[i]);
}

void display2_npk() {
    if (isEmpty2_npk()) {
        printf("Stack 2 is empty.\n");
        return;
    }
    printf("Stack 2 elements (top to bottom):\n");
    for (int i = top2_npk; i < SIZE; i++)
        printf("%d\n", stack_npk[i]);
}

int main_npk() {
    int choice_npk, value_npk, stackChoice_npk;

    while (1) {
        printf("\n========= MULTIPLE STACK MENU =========\n");
        printf("1. Push\n");
        printf("2. Pop\n");
        printf("3. Display\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice_npk);

        switch (choice_npk) {
        case 1:
            printf("Enter stack number (1 or 2): ");
            scanf("%d", &stackChoice_npk);
            printf("Enter value to push: ");
            scanf("%d", &value_npk);
            if (stackChoice_npk == 1)
                push1_npk(value_npk);
            else if (stackChoice_npk == 2)
                push2_npk(value_npk);
            else
                printf("Invalid stack number.\n");
            break;

        case 2:
            printf("Enter stack number (1 or 2): ");
            scanf("%d", &stackChoice_npk);
            if (stackChoice_npk == 1)
                pop1_npk();
            else if (stackChoice_npk == 2)
                pop2_npk();
            else
                printf("Invalid stack number.\n");
            break;

        case 3:
            printf("Enter stack number (1 or 2): ");
            scanf("%d", &stackChoice_npk);
            if (stackChoice_npk == 1)
                display1_npk();
            else if (stackChoice_npk == 2)
                display2_npk();
            else
                printf("Invalid stack number.\n");
            break;

        case 4:
            printf("Exiting program.\n");
            exit(0);

        default:
            printf("Invalid choice! Please try again.\n");
        }
    }

    return 0;
}

int main() {
    return main_npk();
}
```

---

## Output

```
 cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ Assign_23.cpp -o Assign_23 } ; if ($?) { .\Assign_23 }

========= MULTIPLE STACK MENU =========
1. Push
2. Pop
3. Display
4. Exit
Enter your choice: 1
Enter stack number (1 or 2): 1
Enter value to push: 45
45 pushed to Stack 1.

========= MULTIPLE STACK MENU =========
1. Push
2. Pop
3. Display
4. Exit
Enter your choice: 2
Enter stack number (1 or 2): 1
Popped 45 from Stack 1.

========= MULTIPLE STACK MENU =========
1. Push
2. Pop
3. Display
4. Exit
Enter your choice: 3
Enter stack number (1 or 2): 2
Stack 2 is empty.

========= MULTIPLE STACK MENU =========
1. Push
2. Pop
3. Display
4. Exit
Enter your choice: 4
Exiting program.
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## Conclusion

<p>This program demonstrates how two stacks can be implemented in a single array.  
Stack 1 grows from the left, and Stack 2 grows from the right, sharing memory efficiently.  
Overflow occurs when both stacks meet, and underflow occurs when an attempt is made to pop from an empty stack.  
All required operations such as push, pop, overflow, underflow, and display are successfully implemented.</p>

---

