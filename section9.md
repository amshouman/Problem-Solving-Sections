---
layout: default
section_num: "09"
title: Pointer Practice
desc: Practice problems on arrays, pointers, and using pointers in functions.
tags: [pointers, arrays, functions]
---

# 📘 Section 9 — Pointer Practice

 > Practice using pointers with arrays and functions.

---

## 🎯 What You'll Practice

- Moving through an array using a pointer
- Passing arrays to functions
- Returning results from functions
- Updating values through pointer parameters
- Using pointers to find values inside arrays

---

## 🧪 Exercises

---

### Exercise 1: Print Array in Reverse

**Task:** Write a program to print elements in an array on integers in reverse order using a pointer.

<details markdown="1">
<summary>💡 Hint</summary>

- Pointer can move backward using `ptr--`
- Start from: `arr + size - 1`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

void printReverse(int arr[], int size)
{
    int *ptr = arr + size - 1;

    printf("Reverse: ");
    for (int i = 0; i < size; i++)
    {
        printf("%d ", *ptr);
        ptr--;
    }
    printf("\n");
}

int main()
{
    int arr[] = {1, -2, 3, 4, -5, 3, 1};
    int size = sizeof(arr) / sizeof(arr[0]);

    printReverse(arr, size);

    return 0;
}
```

</details>

---

### Exercise 2: Sum of Array Elements

**Task:** Write a function that calculates the sum of an array using pointers.

<details markdown="1">
<summary>💡 Hint</summary>

- Use pointer arithmetic: `*(arr + i)`
- Accumulate values in a `sum` variable

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int sumArray(int arr[], int size)
{
    int sum = 0;

    for (int i = 0; i < size; i++)
    {
        sum += *(arr + i);
    }

    return sum;
}
```

</details>

---

### Exercise 3: Count Even Numbers

**Task:** Write a function that counts how many elements are even in an array.

<details markdown="1">
<summary>💡 Hint</summary>

- Even number condition: `% 2 == 0`
- Traverse using pointer instead of indexing

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int countEven(int arr[], int size)
{
    int count = 0;

    for (int i = 0; i < size; i++)
    {
        if (*(arr + i) % 2 == 0)
        {
            count++;
        }
    }

    return count;
}
```

</details>

---

### Exercise 4: Count Positive and Negative Numbers

**Task:** Write a function that counts positive and negative numbers in an array using pointers.

<details markdown="1">
<summary>💡 Hint</summary>

- Use pointers to modify values: `(*pos)++`
- Check: `> 0` and `< 0`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
void countPosNeg(int arr[], int size, int *pos, int *neg)
{
    *pos = 0;
    *neg = 0;

    for (int i = 0; i < size; i++)
    {
        if (*(arr + i) > 0)
            (*pos)++;
        else if (*(arr + i) < 0)
            (*neg)++;
    }
}
```

</details>

---

### Exercise 5: Find Maximum and Minimum

**Task:** Write a function that takes an integer array and its size as parameters and updates two integer pointers to point to the maximum and minimum values in the array.

<details markdown="1">
<summary>💡 Hint</summary>

- Start with first element as initial max and min
- Compare each element and update values using `*`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
void findMinMax(int arr[], int size, int *maxPtr, int *minPtr)
{
    *maxPtr = arr[0];
    *minPtr = arr[0];

    for (int i = 1; i < size; i++)
    {
        if (arr[i] > *maxPtr)
            *maxPtr = arr[i];

        if (arr[i] < *minPtr)
            *minPtr = arr[i];
    }
}
```

</details>

---

### Exercise 6: Palindrome Array

**Task:** Write a function that checks if an array is a palindrome using pointers.

<details markdown="1">
<summary>💡 Hint</summary>

- Use two pointers: start & end
- Move inward: `start++`, `end--`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int isPalindrome(int arr[], int size)
{
    int *start = arr;
    int *end = arr + size - 1;

    while (start < end)
    {
        if (*start != *end)
            return 0;

        start++;
        end--;
    }

    return 1;
}
```

</details>

---

### Exercise 7: Count Numbers Greater Than Average

**Task:** Write a function that counts how many numbers are greater than the average of the array.

<details markdown="1">
<summary>💡 Hint</summary>

- First compute sum → then average
- Compare each element with average

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int countGreaterThanAvg(int arr[], int size)
{
    int sum = 0;

    for (int i = 0; i < size; i++)
    {
        sum += *(arr + i);
    }

    float avg = (float)sum / size;

    int count = 0;
    for (int i = 0; i < size; i++)
    {
        if (*(arr + i) > avg)
            count++;
    }

    return count;
}
```

</details>

---

> ⬅️ [Back to Home](index.html)
