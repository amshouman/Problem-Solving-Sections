---
layout: default
section_num: "05"
title: Functions
desc: Defining reusable code blocks, passing parameters, return values, and variable scope.
tags: [void, return, parameters]
---

# 📘 Section 5 — Functions

 > Learn how to define reusable code blocks, pass data through parameters, and build modular programs.

---

## 🎯 What You'll Learn

- What functions are and why we use them
- How to define and call functions
- The difference between **formal** and **actual** parameters
- How to use **return values**
- Calling functions with **call by value**

---

## 1. What Is a Function?

A function is a block of code which only runs when it is called. Data can be passed to the function and this data is known as parameters. Define the code once and use it many times.

---

## 2. Your First Function

Here's the simplest example — a function that prints a message:

```c
#include <stdio.h>

void fun() {
    printf("hi");
}

int main() {
    fun();
    return 0;
}
```

| Part | Meaning |
|------|---------|
| `void` | The function does **not** return a value |
| `fun` | The name of the function |
| `()` | No parameters are needed |
| `fun();` | This is how we **call** (execute) the function |

---

## 3. Functions with Parameters

You can pass data to a function using **parameters**:

```c
#include <stdio.h>

void fun(int a) {         // formal parameters
    printf("%d", a);
}

int main() {
    int a = 5;
    fun(a);               // actual parameters
    return 0;
}
```

### Formal vs Actual Parameters

| Term | Where? | Description |
|------|--------|-------------|
| **Formal parameter** | In the function definition | The variable name used _inside_ the function |
| **Actual parameter** | At the call site | The value or variable you _pass_ to the function |

---

## 4. Calling Methods

| Method | Description |
|--------|-------------|
| **Call by Value** | A copy of the value is passed. The original variable is unchanged. |
| **Call by Reference** | The memory address is passed (using pointers). Changes affect the original. |

> 📌 In this section we focus on **Call by Value**. You'll learn Call by Reference when we cover **Pointers**.

---

## 🧪 Exercises — Trace the Output

Practice reading code carefully. Try to predict the output **before** revealing the answer!

---

### Exercise 1: Single Parameter

```c
void Fun(int y) {
    printf("y = %d\n", y);
}

int main() {
    Fun(5);        // first call

    int x = 6;
    Fun(x);        // second call
    Fun(x + 1);    // third call

    return 0;
}
```

<details markdown="1">
<summary>🟢 Click to Show Answer</summary>

**Output:**

```
y = 5
y = 6
y = 7
```

**Explanation:**

- `Fun(5)` → `y` receives `5`, prints `y = 5`
- `Fun(x)` → `x` is `6`, so `y` receives `6`, prints `y = 6`
- `Fun(x + 1)` → `x + 1` = `7`, so `y` receives `7`, prints `y = 7`

</details>

---

### Exercise 2: Two Parameters — Watch the Order!

```c
void Fun(int y, int x) {
    printf("x = %d\ny = %d\n", x, y);
}

int main() {
    int x = 25, y = 13;
    printf("x = %d\ny = %d\n", x, y);
    Fun(x, y);

    return 0;
}
```

<details markdown="1">
<summary>🟢 Click to Show Answer</summary>

**Output:**

```
x = 25
y = 13
x = 13
y = 25
```

**Explanation:**

This is a tricky one! Pay close attention to the **order of parameters**:

1. In `main()`, we print `x = 25` and `y = 13` — straightforward.
2. When we call `Fun(x, y)`, the value of `x` (which is `25`) goes into the **first** parameter of `Fun`, which is named `y`. The value of `y` (which is `13`) goes into the **second** parameter, which is named `x`.
3. So inside `Fun`: `y = 25` and `x = 13`.
4. The `printf` inside `Fun` prints `x` first, then `y` — giving us `x = 13`, `y = 25`.

> ⚠️ **Lesson:** Parameter names inside a function are **independent** of variable names outside it. What matters is the **order** in which values are passed!

</details>

---

### Exercise 3: Local Variable Scope

```c
void Fun(int y) {
    int x = 100;
    printf("x = %d\ny = %d\n", x, y);
}

int main() {
    int x = 25, y = 13;
    printf("x = %d\ny = %d\n", x, y);
    Fun(x);

    return 0;
}
```

<details markdown="1">
<summary>🟢 Click to Show Answer</summary>

**Output:**

```
x = 25
y = 13
x = 100
y = 25
```

**Explanation:**

1. In `main()`: `x = 25`, `y = 13` → prints `x = 25` and `y = 13`.
2. `Fun(x)` is called with `x = 25`, so `Fun`'s parameter `y` receives `25`.
3. Inside `Fun`, a **local** variable `x = 100` is created — this is completely separate from `main`'s `x`.
4. So `Fun` prints `x = 100` and `y = 25`.

> ⚠️ **Lesson:** Each function has its own **scope**. A variable named `x` inside `Fun` is **not** the same as `x` in `main`.

</details>

---

## 🛠️ Coding Exercises

---

### Exercise 4: Hours to Seconds Converter

**Task:** Write a function called `ToSeconds()` that converts hours to seconds. The function should take in one integer parameter representing the number of hours and returns the equivalent number of seconds. Using the above function, calculate how many seconds are there in a day, week, and month.

<details markdown="1">
<summary>💡 Hint</summary>

- 1 hour = 60 minutes × 60 seconds = 3600 seconds
- 1 day = 24 hours
- 1 week = 7 × 24 hours
- 1 month ≈ 30 × 24 hours

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int ToSeconds(int hours) {
    return hours * 60 * 60;
}

int main() {
    int hours = 24;
    int seconds = ToSeconds(hours);
    printf("%d hours = %d seconds\n", hours, seconds);

    int hoursInDay   = 24;       // 1 day = 24 hours
    int hoursInWeek  = 7 * 24;   // 1 week = 7 days = 7 * 24 hours
    int hoursInMonth = 30 * 24;  // 1 month = 30 days = 30 * 24 hours

    printf("Hours in 1 day = %d\n", ToSeconds(hoursInDay));
    printf("Hours in 1 week = %d\n", ToSeconds(hoursInWeek));
    printf("Hours in 1 month = %d\n", ToSeconds(hoursInMonth));

    return 0;
}
```

**Key takeaway:** The function `ToSeconds` is called multiple times with different values. This is the power of functions — write once, reuse everywhere.

</details>

---

### Exercise 5: Quad Root Calculator

**Task:** Using the built-in math function `sqrt()`, write the function `Quadroot()` that returns the quad root (⁴√) of an integer.

> 💡 Recall: ⁴√n = √(√n) — apply the square root **twice**.

<details markdown="1">
<summary>💡 Hint</summary>

- Include `<math.h>` to use `sqrt()`
- The 4th root of a number is the square root of its square root
- Handle the case where the input is **negative** (no real 4th root exists)

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>
#include <math.h>    // needed for the use of sqrt function

double Quadroot(int num) {
    return sqrt(sqrt(num));
}

int main() {
    int num;
    printf("Enter a number to calculate its quad root: ");
    scanf("%d", &num);

    if (num < 0) {
        printf("Negative number quad root is not a real number\n");
    } else {
        double quadroot = Quadroot(num);
        printf("Quad root = %.2f\n", quadroot);
    }

    return 0;
}
```

**Example run:**

```
Enter a number to calculate its quad root: 81
Quad root = 3.00
```

**Why does this work?**
- `sqrt(81)` = `9`
- `sqrt(9)` = `3`
- So ⁴√81 = 3 ✓

</details>

---

## 📋 Quick Reference

| Concept | Syntax |
|---------|--------|
| Void function (no return) | `void funcName() { ... }` |
| Function with return | `int funcName() { return value; }` |
| With parameters | `void funcName(int a, int b) { ... }` |
| Calling a function | `funcName(arg1, arg2);` |
| Using return value | `int result = funcName(arg);` |

---

> ⬅️ [Back to Home](index.html)
