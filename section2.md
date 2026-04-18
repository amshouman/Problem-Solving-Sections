---
layout: default
section_num: "02"
title: Loops
desc: While, for, and do-while loops, with practice on tracing and repetition.
tags: [for, while, do-while]
---

# 📘 Section 2 — Loops

 > Learn how to repeat actions with `while`, `for`, and `do-while` loops.

---

## 🎯 What You'll Learn

- Why loops are essential in programming
- Three types of loops: `while`, `for`, `do-while`
- How to trace loops step by step
- How to use loops with conditions and counters

---

## 1. Why Loops?

A loop is a sequence of instructions that keeps repeating until a certain condition is reached.

![Loop concept](assets/section2/loop-concept.png)

Imagine you need to print numbers from 1 to 1000. Without loops:

```c
printf("number1: %d\n", 1);
printf("number2: %d\n", 2);
printf("number3: %d\n", 3);
// ... 997 more lines!
```

Now assume we need to print from 1 to 1000! Loops let you do this in just a few lines.

---

## 2. While Loop

```c
while (condition) {
    /* code */
}
```

The condition is checked **before** each iteration. The loop repeats as long as the condition is true.

---

## 3. For Loop

```c
for (initialization; condition; update) {
    /* code */
}
```

| Part | Purpose |
|------|---------|
| Initialization | Initializing a new variable to use inside the loop |
| Condition | Setting the condition to exit the loop |
| Update | Updating the variable after each iteration until condition is met |

---

## 4. Do-While Loop

```c
do {
    /* code */
} while (condition);
```

The condition is checked **after** each iteration, so the body runs **at least once**.

## 🧪 Exercises

---

### Exercise 1: Print 1–20 with While Loop

**Task:** Print the integers from 1 to 20 using a while loop and the counter variable x. Print only **5 integers per line**.

<details markdown="1">
<summary>💡 Hint</summary>

- Use the modulus operator `%` to detect every 5th number
- When `x % 5 == 0`, print a newline

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int x = 1;
    while (x <= 20) {
        printf("%d ", x);
        if (x % 5 == 0) {
            printf("\n");
        }
        x++;
    }
    return 0;
}
```

**Output:**

```
1 2 3 4 5 
6 7 8 9 10 
11 12 13 14 15 
16 17 18 19 20 
```

</details>

---

### Exercise 2: Trace the Switch in a Loop

**Task:** What will the output of the following code be?

```c
for (int k = 7; k <= 16; k++)
    switch (k % 10) {
        case 0: printf(", ");       break;
        case 1: printf("OFTEN ");   break;
        case 2:
        case 8: printf("IS ");      break;
        case 3: printf("NOT ");     break;
        case 4:
        case 9: printf("DONE ");    break;
        case 5: printf("WELL");     break;
        case 6: printf(".");        break;
        case 7: ("WHAT ");          break;
        default: printf("Bad number. ");
    }
printf("\n");
```

<details markdown="1">
<summary>🟢 Click to Show Answer</summary>

Let's trace each value of `k`:

| k | k % 10 | Output |
|---|--------|--------|
| 7 | 7 | nothing |
| 8 | 8 | `IS ` |
| 9 | 9 | `DONE ` |
| 10 | 0 | `, ` |
| 11 | 1 | `OFTEN ` |
| 12 | 2 | `IS ` |
| 13 | 3 | `NOT ` |
| 14 | 4 | `DONE ` |
| 15 | 5 | `WELL` |
| 16 | 6 | `.` |

**Final output:**

```
IS DONE , OFTEN IS NOT DONE WELL.
```

> 💡 Notice: `case 7` has `("WHAT ");` but no `printf`, so it does not print anything. Cases 2 & 8 share the same code, and cases 4 & 9 also share code.

</details>

---

### Exercise 3: Divisible by 5, Not by 9

**Task:** Write a C program to print all the integer numbers that are divisible by 5 and not divisible by 9 in the range 1 to 100.

<details markdown="1">
<summary>💡 Hint</summary>

- Divisible by 5: `i % 5 == 0`
- NOT divisible by 9: `i % 9 != 0`
- Combine with `&&`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    for (int i = 1; i <= 100; i++) {
        if (i % 5 == 0 && i % 9 != 0) {
            printf("%d ", i);
        }
    }
    return 0;
}
```

**Output:**

```
5 10 15 20 25 30 35 40 50 55 60 65 70 75 80 85 95 100
```

> Notice that `45` and `90` are missing — they're divisible by both 5 and 9.

</details>
---

> ⬅️ [Back to Home](index.html)
