---
layout: default
section_num: "06"
title: Pointers
desc: Memory addresses, pointer variables, pointer arithmetic, and passing by reference.
tags: [pointers, "*ptr", "&address"]
---

# 📘 Section 6 — Pointers

 > Understand memory addresses, pointer variables, and how to use pointers with arrays and functions.

---

## 🎯 What You'll Learn

- What pointers are and why they matter
- How to declare and use pointer variables
- Pointer arithmetic with arrays
- Passing pointers to functions

---

## 1. Some Pointers Usage

- Dynamic memory allocation
- Passing parameters to functions
- Arrays and strings
- File handling
- Pointer Arithmetic and Complex Data Structures

---

## 2. What Is a Pointer?

A **pointer** is a variable that stores the **memory address** of another variable.

```c
#include <stdio.h>

int main() {
    int x = 10;
    int *p = &x;
    *p = 20;       // changes x to 20 through the pointer
    return 0;
}
```

| Expression | Meaning |
|------------|---------|
| `x` | The value of `x` |
| `&x` | The memory **address** of `x` |
| `p` | The address stored in the pointer (same as `&x`) |
| `*p` | The value **at** that address (same as `x`) |

### Printing Pointer Info

```c
int num = 42;
int *ptr = &num;

printf("Value of num: %d\n", num);        // Output the value of 'num'
printf("Address of num: %p\n", &num);     // Output the address of 'num'
printf("Value stored in ptr: %p\n", ptr); // Output the value stored in the pointer
printf("Value pointed to by ptr: %d\n", *ptr); // Output the value pointed to by the pointer
```

---

## 3. Pointers and Arrays

An array name acts as a pointer to its first element:

```c
int arr[] = {1, 2, 3, 4, 5};
int *ptr = arr;

for (int i = 0; i < 5; i++) {
    printf("%d ", *(ptr + i));
}
```

| Expression | Equivalent | Value |
|------------|-----------|-------|
| `*(ptr + 0)` | `arr[0]` | 1 |
| `*(ptr + 1)` | `arr[1]` | 2 |
| `*(ptr + 2)` | `arr[2]` | 3 |

> 💡 `ptr + i` moves the pointer forward by `i` elements (not `i` bytes — C handles the size automatically).

---

## 🧪 Exercises

---

### Exercise 1: Print Array Using a Pointer

**Task:** Write a program in C to store n elements in an array and print the elements using a pointer.

<details markdown="1">
<summary>💡 Hint</summary>

- Declare a pointer to the array: `int *ptr = arr;`
- Use `*(ptr + i)` to access each element

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter number of elements: ");
    scanf("%d", &n);
    int arr[n];

    printf("Enter %d elements: ", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    int *ptr = arr;
    printf("Array elements: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", *(ptr + i));
    }

    return 0;
}
```

</details>

---

### Exercise 2: Sum & Average with Pointers

**Task:** Create a program that uses pointers to find the sum and average of elements in an array.

<details markdown="1">
<summary>💡 Hint</summary>

- Traverse the array using pointer arithmetic
- Sum all elements, then divide by `n` for the average
- Use `float` or `double` for the average

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter number of elements: ");
    scanf("%d", &n);
    int arr[n];

    printf("Enter %d elements: ", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    int *ptr = arr;
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += *(ptr + i);
    }

    printf("Sum = %d\n", sum);
    printf("Average = %.2f\n", (float)sum / n);

    return 0;
}
```

</details>

---

### Exercise 3: Copy Array Using Pointers

**Task:** Write a program that uses pointers to copy one array to another.

<details markdown="1">
<summary>💡 Hint</summary>

- Create two arrays and two pointers
- Loop through and assign `*(dest + i) = *(src + i)`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter number of elements: ");
    scanf("%d", &n);

    int src[n], dest[n];
    printf("Enter %d elements: ", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &src[i]);
    }

    int *pSrc = src;
    int *pDest = dest;
    for (int i = 0; i < n; i++) {
        *(pDest + i) = *(pSrc + i);
    }

    printf("Copied array: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", dest[i]);
    }

    return 0;
}
```

</details>

---

### Exercise 4: Swap Two Numbers Using Pointers

**Task:** Write a function that takes two integer pointers and swaps the values of the numbers.

<details markdown="1">
<summary>💡 Hint</summary>

- The function signature should be `void swap(int *a, int *b)`
- Use a temporary variable to hold one value during the swap
- Call with `swap(&x, &y)` from `main`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int x = 10, y = 20;
    printf("Before: x = %d, y = %d\n", x, y);

    swap(&x, &y);

    printf("After:  x = %d, y = %d\n", x, y);
    return 0;
}
```

**Output:**

```
Before: x = 10, y = 20
After:  x = 20, y = 10
```

> 💡 This is **call by reference** — the function modifies the original variables because it has their addresses, not copies.

</details>

---

### Exercise 5: Find Min & Max Using Pointers

**Task:** Write a function that takes an integer array and its size as parameters and updates two integer pointers to point to the maximum and minimum values in the array.

<details markdown="1">
<summary>💡 Hint</summary>

- Function signature: `void findMinMax(int *arr, int size, int *max, int *min)`
- Initialize `*max` and `*min` to the first element
- Loop through and update using `*max` and `*min`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

void findMinMax(int *arr, int size, int *max, int *min) {
    *max = arr[0];
    *min = arr[0];

    for (int i = 1; i < size; i++) {
        if (arr[i] > *max) {
            *max = arr[i];
        }
        if (arr[i] < *min) {
            *min = arr[i];
        }
    }
}

int main() {
    int arr[] = {3, 7, 1, 9, 2, 8, 4};
    int size = 7;
    int max, min;

    findMinMax(arr, size, &max, &min);

    printf("Max = %d\n", max);
    printf("Min = %d\n", min);

    return 0;
}
```

**Output:**

```
Max = 9
Min = 1
```

> 💡 By passing `&max` and `&min`, the function can write results directly into `main`'s variables — no return value needed for multiple outputs.

</details>

---

## 📋 Quick Reference

| Concept | Syntax |
|---------|--------|
| Declare pointer | `int *ptr;` |
| Get address | `ptr = &variable;` |
| Dereference (get value) | `*ptr` |
| Pointer arithmetic | `*(ptr + i)` is same as `arr[i]` |
| Pass by reference | `void func(int *p)` called with `func(&x)` |

---

> ⬅️ [Back to Home](index.html)
