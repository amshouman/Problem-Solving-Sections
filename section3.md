---
layout: default
section_num: "03"
title: "Practice: Conditionals & Arrays"
desc: Hands-on exercises — searching, summing, reversing, and checking palindromes in arrays.
tags: [search, max, palindrome]
---

# 📘 Section 3 — Practice: Conditionals & 1D Arrays

 > Put your skills to the test with exercises covering conditional logic and one-dimensional arrays.

---

## 🎯 What You'll Practice

- Using `if-else` for decision-making
- Declaring and traversing arrays
- Searching, summing, and filtering array elements
- Checking patterns in arrays (palindrome)

---

## 🧪 Exercises

---

### Exercise 1: Cartesian Plane Quadrant

**Task:** Accept the x-y coordinates of a point in the Cartesian plane and print a message telling either an axis on which the point lies or the quadrant in which it is found.

**Sample outputs:**

```
(-1.0, -2.5) is in quadrant III
(0, 4.8) is on the y-axis
```

<details markdown="1">
<summary>💡 Hint</summary>

- If both x and y are 0 → origin
- If x is 0 → y-axis
- If y is 0 → x-axis
- Otherwise, check signs to determine the quadrant (I through IV)

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    double x, y;
    printf("Enter the x coordinate: ");
    scanf("%lf", &x);
    printf("Enter the y coordinate: ");
    scanf("%lf", &y);

    if (x == 0 && y == 0) {
        printf("(0,0) is at the origin");
    } else if (x == 0) {
        printf("(0,%.1f) is on the y-axis", y);
    } else if (y == 0) {
        printf("(%.1f,0) is on the x-axis", x);
    } else if (x > 0 && y > 0) {
        printf("(%.1f,%.1f) is in quadrant I", x, y);
    } else if (x < 0 && y > 0) {
        printf("(%.1f,%.1f) is in quadrant II", x, y);
    } else if (x < 0 && y < 0) {
        printf("(%.1f,%.1f) is in quadrant III", x, y);
    } else if (x > 0 && y < 0) {
        printf("(%.1f,%.1f) is in quadrant IV", x, y);
    }

    return 0;
}
```

> 💡 **Key idea:** Check the special cases (origin, axes) **before** checking quadrants. Use `%lf` in `scanf` for `double`.

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
