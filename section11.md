---
layout: default
section_num: "11"
title: Recursion
desc: Introduction to recursion, the call hierarchy, and revision problems on functions.
tags: [recursion, functions, base case, factorial]
---

# 📘 Section 11 — Recursion

 > A function that calls itself. Solve a big problem by reducing it to a smaller version of the same problem — until you hit a case so small you can answer it directly.

---

## 🎯 What You'll Practice

- Understanding what recursion is and how the call stack works
- Writing a **base case** and a **recursive case**
- Tracing recursive calls step-by-step
- Revising functions: sum, digit count, factorial, Fibonacci, palindrome, array printing
- Building a simple calculator that combines several functions

---

## 1. What Is Recursion?

**Recursion** is when a function calls itself to solve a smaller version of the same problem.

Every recursive function must have **two** parts:

1. **Base case** — the stopping condition. A case so small we can answer it directly, without another recursive call.
2. **Recursive case** — the function calls itself with a smaller / simpler input, getting closer to the base case.

> ⚠️ **Without a base case, recursion never stops** — the program keeps calling itself until the call stack runs out of memory (stack overflow).

### General Template Example

```c
returnType functionName(parameters) {
    if (base_case_condition) {
        return base_case_value;          // stop here
    }
    return something + functionName(smaller_input);   // recursive call
}
```

---

## 2. How the Call Hierarchy Works — `fact(5)`

Let's trace the classic example: computing the factorial of 5.
> The factorial of `n` (written `n!`) is the product of all positive integers from `1` up to `n`. For example, `5! = 5 × 4 × 3 × 2 × 1 = 120`. By convention, `0! = 1`.

```c
int fact(int n) {
    if (n == 0)
        return 1;                      // base case
    return n * fact(n - 1);       // recursive case
}
```

Each call **pauses** and waits for the smaller call below it to finish. When the base case finally returns, the results bubble back up.
<br>
**Below you will find a lot of ways to trace recursion and know how it works.**

### Function Calls

> **Note:** It is better to view this diagram on your laptop.

<div style="
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: 50px;
    align-items: start;
    margin: 20px 0;
">

    <!-- LEFT SIDE -->
    <div style="text-align: center;">
        <h3>Phase 1 — Recursive Calls Going Down (Stack Grows)</h3>

        <div style="
            background: var(--bg-card);
            border: 2px solid var(--accent);
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
            box-shadow: 0 4px 12px rgba(0,0,0,0.05);
        ">
            <strong>fact(5)</strong><br>
            <small>needs <strong>5 × fact(4)</strong><br>so it waits for fact(4)</small>
        </div>

        <div style="font-size: 34px; color: var(--text);">↓</div>

        <div style="
            background: var(--bg-card);
            border: 2px solid var(--accent);
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
        ">
            <strong>fact(4)</strong><br>
            <small>needs <strong>4 × fact(3)</strong><br>so it waits for fact(3)</small>
        </div>

        <div style="font-size: 34px; color: var(--text);">↓</div>

        <div style="
            background: var(--bg-card);
            border: 2px solid var(--accent);
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
        ">
            <strong>fact(3)</strong><br>
            <small>needs <strong>3 × fact(2)</strong><br>so it waits for fact(2)</small>
        </div>

        <div style="font-size: 34px; color: var(--text);">↓</div>

        <div style="
            background: var(--bg-card);
            border: 2px solid var(--accent);
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
        ">
            <strong>fact(2)</strong><br>
            <small>needs <strong>2 × fact(1)</strong><br>so it waits for fact(1)</small>
        </div>

        <div style="font-size: 34px; color: var(--text);">↓</div>

        <div style="
            background: var(--bg-card);
            border: 2px solid var(--accent);
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
        ">
            <strong>fact(1)</strong><br>
            <small>needs <strong>1 × fact(0)</strong><br>so it waits for fact(0)</small>
        </div>

        <div style="font-size: 34px; color: var(--text);">↓</div>

        <div style="
            background: rgba(255, 193, 7, 0.08);
            border: 2px solid #d9a62d;
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
        ">
            <strong>fact(0)</strong><br>
            <small><strong>Base Case</strong><br>returns <strong>1</strong> immediately</small>
        </div>
    </div>

    <!-- RIGHT SIDE -->
    <div style="text-align: center;">
        <h3>Phase 2 — Returning Values Up (Stack Shrinks)</h3>

        <div style="
            background: var(--bg-card);
            border: 2px solid var(--green);
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
        ">
            <strong>fact(5)</strong><br>
            <small><strong>5 × 24 = 120</strong><br>final answer returned</small>
        </div>

        <div style="font-size: 34px; color: var(--text);">↑</div>

        <div style="
            background: var(--bg-card);
            border: 2px solid var(--green);
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
        ">
            <strong>fact(4)</strong><br>
            <small><strong>4 × 6 = 24</strong><br>returns 24</small>
        </div>

        <div style="font-size: 34px; color: var(--text);">↑</div>

        <div style="
            background: var(--bg-card);
            border: 2px solid var(--green);
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
        ">
            <strong>fact(3)</strong><br>
            <small><strong>3 × 2 = 6</strong><br>returns 6</small>
        </div>

        <div style="font-size: 34px; color: var(--text);">↑</div>

        <div style="
            background: var(--bg-card);
            border: 2px solid var(--green);
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
        ">
            <strong>fact(2)</strong><br>
            <small><strong>2 × 1 = 2</strong><br>returns 2</small>
        </div>

        <div style="font-size: 34px; color: var(--text);">↑</div>

        <div style="
            background: var(--bg-card);
            border: 2px solid var(--green);
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
        ">
            <strong>fact(1)</strong><br>
            <small><strong>1 × 1 = 1</strong><br>returns 1</small>
        </div>

        <div style="font-size: 34px; color: var(--text);">↑</div>

        <div style="
            background: rgba(255, 193, 7, 0.08);
            border: 2px solid #d9a62d;
            border-radius: 22px;
            padding: 20px;
            margin: 15px auto;
            width: 100%;
            max-width: 320px;
            color: var(--text);
        ">
            <strong>Start here</strong><br>
            <small>base case returned <strong>1</strong></small>
        </div>
    </div>

</div>

> 💡 **Phase 1 (left, top-down):** every call **pauses** holding onto its multiplication, waiting for the smaller call beneath it. The call stack keeps growing.
>
> 💡 **Phase 2 (right, bottom-up):** once the base case returns `1`, each paused call **wakes up**, plugs the returned value into its multiplication, and returns to its own caller. The stack shrinks back to empty.

> 💡 **Key idea:** Each call on the way **down** just makes a smaller call and pauses. The real work happens on the way **back up**, once the base case returns a value.

### Trace Tables

Read the first table top-to-bottom, then the second table top-to-bottom.

**Phase 1 — Going Down (calls pause and wait)**

| Current Call | Needs to Compute | Waiting For |
|--------------|------------------|-------------|
| `fact(5)` | `5 * fact(4)` | `fact(4)` |
| `fact(4)` | `4 * fact(3)` | `fact(3)` |
| `fact(3)` | `3 * fact(2)` | `fact(2)` |
| `fact(2)` | `2 * fact(1)` | `fact(1)` |
| `fact(1)` | `1 * fact(0)` | `fact(0)` |
| `fact(0)` | base case hit | returns `1` immediately |

**Phase 2 — Coming Back Up (values bubble up)**

| Current Call | Receives From Below | Computes | Returns |
|--------------|---------------------|----------|---------|
| `fact(0)` | — | base case | `1` |
| `fact(1)` | `1` | `1 * 1` | `1` |
| `fact(2)` | `1` | `2 * 1` | `2` |
| `fact(3)` | `2` | `3 * 2` | `6` |
| `fact(4)` | `6` | `4 * 6` | `24` |
| `fact(5)` | `24` | `5 * 24` | `120` ✅ |

### Substitution Trace

Another way to see it — watch the expression unfold step by step:

```
fact(5)
= 5 * fact(4)
= 5 * 4 * fact(3)
= 5 * 4 * 3 * fact(2)
= 5 * 4 * 3 * 2 * fact(1)
= 5 * 4 * 3 * 2 * 1 * fact(0)
= 5 * 4 * 3 * 2 * 1 * 1
= 5 * 4 * 3 * 2 * 1
= 5 * 4 * 3 * 2
= 5 * 4 * 6
= 5 * 24
= 120
```

### Call Tree

Because `fact` makes **only one** recursive call, its "tree" is actually just a straight line:

```
fact(5)
    │
    └── fact(4)
            │
            └── fact(3)
                    │
                    └── fact(2)
                            │
                            └── fact(1)
                                    │
                                    └── fact(0)   ← base case
```

> 💡 Keep this shape in mind — later, when you meet **Fibonacci** in Exercise 6, you'll see what happens when a function calls itself **twice** in one line. The tree stops being a line and starts **branching**.

---

## 🧪 Exercises

---

### Exercise 1: Sum of First N Natural Numbers

**Task:** Write a recursive function to calculate the sum of the first `n` natural numbers.

<details markdown="1">
<summary>💡 Hint</summary>

- **Base case:** when `n == 0`, the sum is `0` — return it.
- **Recursive case:** `sum(n) = n + sum(n - 1)`.
- Each call reduces `n` by 1 until it reaches `0`.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int sum(int n){
    if (n == 0)
    {
        return 0;
    }
    return n + sum(n - 1);
}

int main(){
    int n;
    scanf("%d", &n);
    printf("%d", sum(n));
    return 0;
}
```

**Trace for `sum(4)`:**

```
sum(4) = 4 + sum(3)
       = 4 + 3 + sum(2)
       = 4 + 3 + 2 + sum(1)
       = 4 + 3 + 2 + 1 + sum(0)
       = 4 + 3 + 2 + 1 + 0
       = 10
```

</details>

---

### Exercise 2: Count Digits of a Number

**Task:** Using a recursive function, write a program to calculate the number of digits in an integer.

<details markdown="1">
<summary>💡 Hint</summary>

- **Base case:** when `n == 0`, there are no more digits — return `0`.
- **Recursive case:** `1 + countDigits(n / 10)` — chop off the last digit and count the rest.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int countDigits(int n) {
    if (n == 0)
        return 0;                          // base case
    return 1 + countDigits(n / 10);
}

int main() {
    int num = 12345;
    printf("Number of digits is %d\n", countDigits(num));
    return 0;
}
```

**Trace for `countDigits(12345)`:**

```
countDigits(12345) = 1 + countDigits(1234)
                   = 1 + 1 + countDigits(123)
                   = 1 + 1 + 1 + countDigits(12)
                   = 1 + 1 + 1 + 1 + countDigits(1)
                   = 1 + 1 + 1 + 1 + 1 + countDigits(0)
                   = 1 + 1 + 1 + 1 + 1 + 0
                   = 5
```

> ⚠️ This version returns `0` if you pass in `0`. If you want `0` to count as 1 digit, handle it as a special case in `main`.

</details>

---

### Exercise 3: Factorial of N

**Task:** Using a recursive function, write a program to calculate the factorial of `n`.

<details markdown="1">
<summary>💡 Hint</summary>

- **Base case:** `factorial(0) = 1`.
- **Recursive case:** `factorial(n) = n * factorial(n - 1)`.
- See the full call-tree walkthrough in **Section 2** above.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int factorial(int n) {
    if (n == 0)
        return 1;                          // base case
    return n * factorial(n - 1);
}

int main() {
    int n = 5;
    printf("Factorial of number %d is %d\n", n, factorial(n));
    return 0;
}
```

**Output:**

```
Factorial of number 5 is 120
```

</details>

---

### Exercise 4: Palindrome Check (Number)

**Task:** Using a recursive function, write a program to check if a number is palindrome or not.

<details markdown="1">
<summary>💡 Hint</summary>

- First **reverse** the number recursively, then compare it with the original.
- Use two parameters: the number being chopped (`num`) and the reversed-so-far (`rev`).
- **Base case:** when `num == 0`, return `rev`.
- **Recursive case:** `rev = rev * 10 + num % 10`, then call with `num / 10`.

</details>

<details markdown="1">
<summary>💡 Iterative version (for comparison)</summary>

```c
// loop without recursion
int reversed = 0;
while (num != 0) {
    reversed = (reversed * 10) + num % 10;
    num /= 10;
}
```

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int revNum(int num, int rev)
{
    if (num == 0)
        return rev;
    rev = (rev * 10) + (num % 10);
    return revNum(num / 10, rev);
}

int main()
{
    int num;
    scanf("%d", &num);
    if (revNum(num, 0) == num)
        printf("%d is a palindrome.\n", num);
    else
        printf("%d is not a palindrome.\n", num);
    return 0;
}
```

**Examples:**
- `121` → reversed = `121` → **palindrome**
- `12321` → reversed = `12321` → **palindrome**
- `1234` → reversed = `4321` → **not palindrome**

</details>

---

### Exercise 5: Print Array Using Recursion

**Task:** Write a program to print the elements of an array using recursion.

<details markdown="1">
<summary>💡 Hint</summary>

- Pass the array, its size, and an index `i` (starting at `0`).
- **Base case:** when `i == size`, stop.
- **Recursive case:** print `arr[i]`, then call with `i + 1`.
- 💡 **Trick:** If you swap the order (recursive call *before* the `printf`), the array will print in **reverse**!

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

void printRec(int arr[], int size, int i){
    if (i == size)
    {
        return;
    }
    printf("%d ", arr[i]);
    printRec(arr, size, i + 1);
    // if you switch this line with the line above,
    // the array will be printed in reverse
}

int main(){
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    printRec(arr, size, 0);
    return 0;
}
```

**Output:**

```
1 2 3 4 5
```

**Reverse version** — just swap the two lines inside the function:

```c
void printRecReverse(int arr[], int size, int i){
    if (i == size) return;
    printRecReverse(arr, size, i + 1);   // recurse first
    printf("%d ", arr[i]);               // print after
}
// Output: 5 4 3 2 1
```

</details>

---

### Exercise 6: Fibonacci

**Task:** Using a recursive function, write a program that prints the `n`-th Fibonacci number.

The Fibonacci sequence is defined as:

- `fib(0) = 0`
- `fib(1) = 1`

Every other term is simply the sum of its two predecessors 

So the sequence is: `0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...`

> 🔑 **What makes this different?** The recursive case makes **two** calls to itself in the same line. This changes the shape of the call trace — instead of a straight line, it becomes a **tree**.

<details markdown="1">
<summary>💡 Hint</summary>

- You need **two** base cases this time: `fib(0) = 0` and `fib(1) = 1`.
- **Recursive case:** `return fib(n - 1) + fib(n - 2);`
- Since C evaluates left-to-right, `fib(n - 1)` is fully computed **first**, then `fib(n - 2)`.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int fib(int n) {
    if (n <= 1)
        return n;                        // base case (covers fib(0) and fib(1))
    return fib(n - 1) + fib(n - 2);      // TWO recursive calls
}

int main() {
    int n;
    scanf("%d", &n);
    printf("fib of %d = %d\n", n, fib(n));
    return 0;
}
```

**Example:**

```example
Enter n: 4
fib of 4 = 3
```

</details>

#### Substitution Trace for `fib(4)`

When a function calls itself twice, we can't just unfold in a straight line — we need **parentheses** to keep track of which call is being expanded next. On each line, we only expand the **leftmost unresolved call**; the others sit and wait their turn.

```
fib(4)
= fib(3) + fib(2)
= (fib(2) + fib(1)) + fib(2)
= ((fib(1) + fib(0)) + fib(1)) + fib(2)
= ((1 + fib(0)) + fib(1)) + fib(2)
= ((1 + 0) + fib(1)) + fib(2)
= (1 + fib(1)) + fib(2)
= (1 + 1) + fib(2)
= 2 + fib(2)
= 2 + (fib(1) + fib(0))
= 2 + (1 + fib(0))
= 2 + (1 + 0)
= 2 + 1
= 3
```

#### Call Tree for `fib(4)`

```
                    fib(4)
                   /      \
                fib(3)    fib(2)
               /     \    /    \
            fib(2) fib(1) fib(1) fib(0)
            /   \
         fib(1) fib(0)
```

With the values filled in from the bottom up:

```
                     3
                   /   \
                  2     1
                /   \  /  \
               1   1  1    0
              / \
             1   0
```

---

### Exercise 7: Simple Calculator

**Task:** Write a program to perform simple calculator operations. The valid operations are:

| Symbol | Operation      |
|--------|----------------|
| `+`    | Addition       |
| `-`    | Subtraction    |
| `*`    | Multiplication |
| `/`    | Division       |
| `!`    | Factorial      |

The program must contain the following functions:

- **A)** `fact` — takes one input and returns the factorial (recursively).
- **B)** `add` — performs addition of two numbers.
- **C)** `sub` — performs subtraction of two numbers.
- **D)** `mul` — performs multiplication of two numbers.
- **E)** `div` — performs the division of two numbers.

The program must also check for bad input data (division by zero, negative factorial, invalid choice).

**Expected menu:**

```
1: Addition
2: Subtraction
3: Multiplication
4: Division
5: Factorial
6: Quit
```

<details markdown="1">
<summary>💡 Hint</summary>

- Write each operation as its own small function — `main` just reads the choice and calls the right one.
- For **division**, return `double` (cast one operand) so you don't lose the decimal part.
- **Guard checks:** if the user picks division and enters `0` as the divisor → error. If they pick factorial and enter a negative number → error.
- Use `switch` on the choice number. Add a `default` case for invalid options.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int sub(int a, int b) {
    return a - b;
}

int mul(int a, int b) {
    return a * b;
}

double divide(int a, int b) {
    return (double)a / b;
}

int fact(int n) {
    if (n == 0)
        return 1;                     // base case
    return n * fact(n - 1);           // recursive case
}

int main() {
    int c, num1, num2;

    printf("1: Addition\n");
    printf("2: Subtraction\n");
    printf("3: Multiplication\n");
    printf("4: Division\n");
    printf("5: Factorial\n");
    printf("6: Quit\n");

    printf("Enter your operation: ");
    scanf("%d", &c);

    switch (c) {
        case 1:
            printf("Enter two numbers: ");
            scanf("%d %d", &num1, &num2);
            printf("Result: %d\n", add(num1, num2));
            break;
        case 2:
            printf("Enter two numbers: ");
            scanf("%d %d", &num1, &num2);
            printf("Result: %d\n", sub(num1, num2));
            break;
        case 3:
            printf("Enter two numbers: ");
            scanf("%d %d", &num1, &num2);
            printf("Result: %d\n", mul(num1, num2));
            break;
        case 4:
            printf("Enter two numbers: ");
            scanf("%d %d", &num1, &num2);
            if (num2 == 0) {
                printf("Division by zero error\n");
            }
            else {
                printf("Result: %.2f\n", divide(num1, num2));
            }
            break;
        case 5:
            printf("Enter a number: ");
            scanf("%d", &num1);
            if (num1 < 0) {
                printf("Enter a positive number to calculate its factorial\n");
            }
            else {
                printf("Result: %d\n", fact(num1));
            }
            break;
        case 6:
            printf("Goodbye\n");
            break;
        default:
            printf("Incorrect option\n");
    }
    return 0;
}
```

**Sample runs:**

```
Enter your operation: 1
Enter two numbers: 2 3
Result: 5
```

```
Enter your operation: 5
Enter a number: 5
Result: 120
```

```
Enter your operation: 4
Enter two numbers: 10 0
Division by zero error
```

</details>

---

> ⬅️ [Back to Home](index.html)