---
layout: default
section_num: "03"
title: Arrays
desc: One-dimensional arrays, traversal, searching, summing, reversing, and filtering.
tags: [arrays, 1D arrays, search, max, palindrome]
---

# 📘 Section 3 — Arrays

 > Store many values under one name, then process them with loops.

---

## 🎯 What You'll Practice

- Declaring and initializing arrays
- Accessing array elements using indexes
- Traversing arrays with loops
- Searching, summing, reversing, and filtering array elements

---

## 1. Arrays

An array is a data structure consisting of a collection of elements, each identified by an array index.

![Array concept](assets/section3/array-concept.png)

### Why Arrays?

Without arrays, storing 1000 values requires 1000 separate variables:

```c
int number1;
int number2;
// ... now assume we need 1000 variables!
```

### Declaring and Initializing

```c
int array[] = {25, 50, 75, 100};     // Declare with values
int array2[4];                        // Declare with size only
array2[0] = 25;                       // Set value by index
```

### Indexing

Arrays in C are **zero-indexed** — the first element is at position `0`:

```
Index:   [0]   [1]   [2]   [3]
Value:    25    50    75   100
```

## 🧪 Exercises

---

### Exercise 1: Array Operations

**Task:** Initiate an array with the following integer values: `{-5, 3, 0, 1, 27}` then run the following operations on the array and print out the final output:

1. Add 7 to the fourth element
2. Multiply the first element by the third element → store in the fifth element
3. Subtract 2 from the second element
4. Multiply the first element by -1
5. Set the value of the third element to the same value of the first element
6. Add 9 to the fifth element

<details markdown="1">
<summary>💡 Hint</summary>

- Remember: arrays are zero-indexed! The "4th element" is `arr[3]`
- Perform operations **in order** — each step uses results from previous steps

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int arr[] = {-5, 3, 0, 1, 27};

    arr[3] += 7;              // 1 → 8
    arr[4] = arr[0] * arr[2]; // -5 * 0 = 0
    arr[1] -= 2;              // 3 → 1
    arr[0] *= -1;             // -5 → 5
    arr[2] = arr[0];          // 0 → 5
    arr[4] += 9;              // 0 → 9

    for (int i = 0; i < 5; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

**Output:**

```
5 1 5 8 9
```

**Step-by-step trace:**

| Step | arr[0] | arr[1] | arr[2] | arr[3] | arr[4] |
|------|--------|--------|--------|--------|--------|
| Start | -5 | 3 | 0 | 1 | 27 |
| 1 | -5 | 3 | 0 | **8** | 27 |
| 2 | -5 | 3 | 0 | 8 | **0** |
| 3 | -5 | **1** | 0 | 8 | 0 |
| 4 | **5** | 1 | 0 | 8 | 0 |
| 5 | 5 | 1 | **5** | 8 | 0 |
| 6 | 5 | 1 | 5 | 8 | **9** |

</details>

---

### Exercise 2: Reverse an Array

**Task:** Write a program in C to read n number of values in an array and display them in reverse order.

<details markdown="1">
<summary>💡 Hint</summary>

- Read values with a forward loop (`i = 0` to `n-1`)
- Print with a backward loop (`i = n-1` down to `0`)

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int n;
    printf("Enter the number of elements in the array: ");
    scanf("%d", &n);
    int arr[n];

    printf("Enter the numbers of the array: ");
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    for (int i = n - 1; i >= 0; i--) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

</details>

---

### Exercise 3: Sum of Array Elements

**Task:** Write a program in C to find the sum of all elements of the array.

<details markdown="1">
<summary>💡 Hint</summary>

- Initialize `sum = 0` before the loop
- Add each element to `sum` as you read it (or in a separate loop)

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int n, sum = 0;
    printf("Enter the number of elements in the array: ");
    scanf("%d", &n);
    int arr[n];

    printf("Enter the numbers of the array: ");
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
        sum = sum + arr[i];
    }

    printf("sum=%d", sum);
    return 0;
}
```

> 💡 You can accumulate the sum while reading input — no need for a second loop.

</details>

---

### Exercise 4: Search for a Value

**Task:** Check if number 1 appears in an array or not. Print `"true"` if found, `"false"` otherwise.

<details markdown="1">
<summary>💡 Hint</summary>

- Loop through the array
- If you find `1`, print and **immediately return** to stop searching

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int n = 5;
    int arr[] = {2, 3, 1, 4, 5};

    for (int i = 0; i < n; i++) {
        if (arr[i] == 1) {
            printf("true");
            return 0;
        }
    }

    printf("false");
    return 0;
}
```

> 💡 **Early exit pattern:** Using `return 0` inside the loop lets you stop as soon as you find the answer.

</details>

---

### Exercise 5: Find the Largest Element

**Task:** Find the largest element in an array of 10 elements.

<details markdown="1">
<summary>💡 Hint</summary>

- Assume the first element is the max
- Compare every other element — update if larger

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int a[10], max;

    for (int i = 0; i < 10; i++) {
        scanf("%d", &a[i]);
    }

    max = a[0];
    for (int i = 1; i < 10; i++) {
        if (max < a[i]) {
            max = a[i];
        }
    }

    printf("Max = %d", max);
    return 0;
}
```

> ⚠️ **Don't initialize max to 0!** If all values are negative, `0` would incorrectly remain the max. Always start with the first element.

</details>

---

### Exercise 6: Palindrome Check

**Task:** Given a number N and an array A of N numbers. Determine if it's palindrome or not.

<details markdown="1">
<summary>💡 Hint</summary>

- Compare `A[0]` with `A[N-1]`, then `A[1]` with `A[N-2]`, and so on
- You only need to check the first half of the array
- If any pair doesn't match → not a palindrome

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);
    int A[N];

    for (int i = 0; i < N; i++) {
        scanf("%d", &A[i]);
    }

    for (int i = 0; i < N / 2; i++) {
        if (A[i] != A[N - i - 1]) {
            printf("NOT PALINDROME");
            return 0;
        }
    }

    printf("PALINDROME");
    return 0;
}
```

**Example:**
- `{1, 2, 3, 2, 1}` → `A[0]==A[4]`, `A[1]==A[3]` → **PALINDROME**
- `{1, 2, 3, 4, 5}` → `A[0]!=A[4]` → **NOT PALINDROME**

</details>

---

### Exercise 7: Filter by Value

**Task:** Given a number N and an array A of N numbers. Print all array positions that store a number less than or equal to 10 and the number stored in that position.

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int N;
    scanf("%d", &N);
    int A[N];

    for (int i = 0; i < N; i++) {
        scanf("%d", &A[i]);
    }

    printf("Positions and values less than or equal 10:\n");
    for (int i = 0; i < N; i++) {
        if (A[i] <= 10) {
            printf("Position: %d, Value: %d\n", i, A[i]);
        }
    }
    return 0;
}
```

</details>

---

> ⬅️ [Back to Home](index.html)
