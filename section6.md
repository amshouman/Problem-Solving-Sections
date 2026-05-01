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

### How the Pointer Looks in Memory

After `int *p = &x;` and before `*p = 20;`, assume the computer stores `x` at address `1000`, and stores the pointer `p` at address `2000`.

<div class="pointer-diagram" role="img" aria-label="Pointer p stores address 1000, which is the address of variable x.">
  <div class="memory-cell">
    <div class="memory-address">Address 1000</div>
    <div class="memory-box">10</div>
    <div class="memory-name">x</div>
  </div>
  <div class="pointer-arrow">
    <span>p stores this address</span>
  </div>
  <div class="memory-cell">
    <div class="memory-address">Address 2000</div>
    <div class="memory-box">1000</div>
    <div class="memory-name">p</div>
  </div>
</div>

The value inside `p` is `1000`, so `p` stores the address of `x`.

So:

| Expression | Meaning | Value in this example |
|------------|---------|-----------------------|
| `x` | Value stored in `x` | `10` |
| `&x` | Address of `x` | `1000` |
| `p` | Value stored in pointer `p` | `1000` |
| `*p` | Go to address stored in `p` and get the value there | `10` |
| `&p` | Address of the pointer variable itself | `2000` |

> A pointer is also a variable, so it has its **own address**. The special thing about a pointer is that the value inside it is an **address**.
>
> When we write `*p = 20;`, C goes to the address stored inside `p` (`1000`) and changes the value of `x` from `10` to `20`.

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
- Use `*ptr` to access the current element, then move with `ptr++`

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
        printf("%d ", *ptr);
        ptr++;
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
- Use `*ptr` to read the current element, then `ptr++` to move to the next element
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
        sum += *ptr;
        ptr++;
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
- Loop through and assign `*ptr2 = *ptr1`, then increment both pointers

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter number of elements: ");
    scanf("%d", &n);

    int arr1[n], arr2[n];
    printf("Enter %d elements: ", n);
    int *ptr1 = arr1;
    int *ptr2 = arr2;

    for (int i = 0; i < n; i++) {
        scanf("%d", ptr1);
        ptr1++;
    }

    ptr1 = arr1;
    for (int i = 0; i < n; i++) {
        *ptr2 = *ptr1;
        ptr1++;
        ptr2++;
    }

    printf("Copied array: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr2[i]);
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
    int x = 5;
    int y = 3;
    printf("before swap: x= %d, y= %d\n", x, y);

    swap(&x, &y);

    printf("after swap: x= %d, y= %d\n", x, y);
    return 0;
}
```

**Output:**

```
before swap: x= 5, y= 3
after swap: x= 3, y= 5
```

> 💡 This is **call by reference** — the function modifies the original variables because it has their addresses, not copies.

</details>

---

### Exercise 5: Find Min & Max Using Pointers

**Task:** Write a function that takes an integer array and its size as parameters and updates two integer pointers to point to the maximum and minimum values in the array.

<details markdown="1">
<summary>💡 Hint</summary>

- Function signature: `void maxAndMin(int arr[], int size, int *max, int *min)`
- Initialize `*max` and `*min` to the first element
- Loop through and update using `*max` and `*min`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

void maxAndMin(int arr[], int size, int *max, int *min) {
    *max = *min = arr[0];
    for (int i = 1; i < size; i++) {
        if (arr[i] > *max) {
            *max = arr[i];
        } else if (arr[i] < *min) {
            *min = arr[i];
        }
    }
}

int main() {
    int arr[] = {2, 1, 3, 4, 2, 2};
    int size = sizeof(arr) / sizeof(arr[0]);
    int max, min;

    maxAndMin(arr, size, &max, &min);

    printf("Max= %d - Min= %d\n", max, min);

    return 0;
}
```

**Output:**

```
Max= 4 - Min= 1
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
