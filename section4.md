---
layout: default
section_num: "04"
title: 2D Arrays
desc: Two-dimensional arrays, nested loops, matrix operations, and building a sales report.
tags: [2D arrays, matrices, nested loops]
---

# 📘 Section 4 — 2D Arrays

 > Expand your array skills into two dimensions — rows, columns, matrices, and tabular data.

---

## 🎯 What You'll Learn

- How to declare and initialize 2D arrays
- Navigating rows and columns with nested loops
- Working with matrices (comparison, row operations)
- Building a real-world sales report

---

## 1. Two-Dimensional Arrays

A 2D array is like a **table** with rows and columns:

```c
// int array[row][col];
// int array[][col];
int array[][3] = {
    {25, 50, 100},
    {12, 20,  32}
};
```

This creates a 2×3 table:

|  | Col 0 | Col 1 | Col 2 |
|--|-------|-------|-------|
| **Row 0** | 25 | 50 | 100 |
| **Row 1** | 12 | 20 | 32 |

> 💡 You can omit the **row** count when initializing with values, but you must always specify the **column** count.

### Accessing Elements

```c
array[0][2]  // → 100 (row 0, column 2)
array[1][0]  // → 12  (row 1, column 0)
```

### Traversing with Nested Loops

```c
for (int i = 0; i < 2; i++) {        // rows
    for (int j = 0; j < 3; j++) {    // columns
        printf("%d ", array[i][j]);
    }
    printf("\n");
}
```

---

## 🧪 Exercises

---

### Exercise 1: Sales Report

**Task:** A company has four salespeople (1 to 4) who sell five different products (1 to 5). Once a day, each salesperson passes in a slip for each different type of product sold. Each slip contains the salesperson number, the product number, and the total dollar value of that product sold that day.

Write a program that reads all this sales information and summarizes the total sales by salesperson by product. All totals should be stored in the two-dimensional array `sales`. After processing all the information, print the results in tabular format with each column representing a particular salesperson and each row representing a particular product. Cross-total each row to get the total sales of each product; cross-total each column to get the total sales by salesperson.

<details markdown="1">
<summary>💡 Hint</summary>

- Use `sales[product-1][salesperson-1]` to map 1-based input to 0-based indices
- Use `+= amount` to accumulate sales for the same product/salesperson combo
- Create a separate array `totalSalesPerPerson[4]` for column totals
- Use `while(1)` with `break` to handle unknown number of inputs until user enters `-1`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    double sales[5][4] = {0};
    int salesperson, product;
    double amount;

    printf("Enter salesperson (1-4), product (1-5), and sales amount.\n");
    printf("Enter -1 to stop:\n");

    while (1) {
        scanf("%d", &salesperson);
        if (salesperson == -1) {
            break;
        }
        scanf("%d%lf", &product, &amount);
        sales[product - 1][salesperson - 1] += amount;
    }

    printf("\nSales Report\n");

    double totalSalesPerPerson[4] = {0};
    double totalOfProduct;

    for (int i = 0; i < 5; i++) {
        totalOfProduct = 0;
        for (int j = 0; j < 4; j++) {
            printf("%7.1f", sales[i][j]);
            totalOfProduct += sales[i][j];
            totalSalesPerPerson[j] += sales[i][j];
        }
        printf("%12.1f\n", totalOfProduct);
    }

    printf("----------------------------------------------\n");

    double totalSales = 0;
    for (int j = 0; j < 4; j++) {
        printf("%7.1f", totalSalesPerPerson[j]);
        totalSales += totalSalesPerPerson[j];
    }
    printf("%12.1f\n", totalSales);

    return 0;
}
```

**Key concepts:**
- `while (1)` with `break` — loop until the user enters `-1`
- `%7.1f` — 7 total places, 1 after the decimal point (aligns columns nicely)
- `%lf` is for `double` in `scanf`
- Cross-totals track both row sums (per product) and column sums (per salesperson)

</details>

---

### Exercise 2: Matrix Equality

**Task:** Write a C program that checks if 2 matrices 3×3 entered by the user are equal or not.

<details markdown="1">
<summary>💡 Hint</summary>

- Use nested loops to read both matrices
- Compare element by element — if any pair differs, print "NOT EQUAL" and exit immediately

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int m1[3][3], m2[3][3];

    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            scanf("%d", &m1[i][j]);

    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            scanf("%d", &m2[i][j]);

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (m1[i][j] != m2[i][j]) {
                printf("NOT EQUAL MATRIX");
                return 0;
            }
        }
    }

    printf("EQUAL MATRIX");
    return 0;
}
```

> 💡 **Early exit:** As soon as one pair doesn't match, we know the result — no need to keep checking.

</details>

---

### Exercise 3: Maximum per Row

**Task:** Find maximum element of each row in a matrix.

<details markdown="1">
<summary>💡 Hint</summary>

- For each row, assume the first element is the max
- Compare all elements in that row and update if larger

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main() {
    int arr[3][5] = {
        {10, 2, 3, 4, 4},
        { 1, 2, 1, 3, 3},
        { 3, 2, 5, 7, 8}
    };

    for (int i = 0; i < 3; i++) {
        int max = arr[i][0];
        for (int j = 0; j < 5; j++) {
            if (arr[i][j] > max) {
                max = arr[i][j];
            }
        }
        printf("Max element in row number %d equal %d\n", i + 1, max);
    }

    return 0;
}
```

**Output:**

```
Max element in row number 1 equal 10
Max element in row number 2 equal 3
Max element in row number 3 equal 8
```

> 💡 This is the same "find max" pattern from 1D arrays, applied **once per row** using the outer loop.

</details>

---

## 📋 Quick Reference

| Task | Pattern |
|------|---------|
| Declare 2D array | `int arr[rows][cols];` |
| Initialize with values | `int arr[][3] = { {1,2,3}, {4,5,6} };` |
| Access element | `arr[row][col]` |
| Traverse all elements | Nested `for` loops (outer = rows, inner = cols) |
| Row total | Sum inner loop, reset before each row |
| Column total | Use a separate array, accumulate across rows |

---

> ⬅️ [Back to Home](index.html)
