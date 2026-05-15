---
layout: default
section_num: "13"
title: Sorting and Searching
desc: Linear search, binary search, selection sort, and bubble sort — the classic algorithms for finding and ordering data in arrays.
tags: [searching, sorting, linear search, binary search, selection sort, bubble sort]
---

# 📘 Section 13 — Sorting and Searching

 > Two of the most common tasks you'll ever do with an array — **find** something inside it, and **arrange** it in order.

---

## 🎯 What You'll Practice

- Searching for a value inside an array using **Linear Search** and **Binary Search**
- Sorting an array using **Selection Sort** and **Bubble Sort**
- Understanding when each algorithm is appropriate (sorted vs. unsorted data)
- Tracing each algorithm step-by-step on a small array

---

## 1. Overview — Four Classic Algorithms

| Category | Algorithm | Requires Sorted Array? | Idea |
|----------|-----------|------------------------|------|
| Searching | Linear Search | ❌ No | Check each element one by one |
| Searching | Binary Search | ✅ Yes | Repeatedly cut the search range in half |
| Sorting   | Selection Sort | — | Pick the smallest each pass, place it at the front |
| Sorting   | Bubble Sort | — | Swap adjacent pairs until the array is sorted |

---

## 2. Linear Search

**Idea:** Walk through the array from left to right. Compare every element with the target. Stop as soon as you find a match.

```c
int LinearSearch(int arr[], int n, int target) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == target) {
            return i;        // found — return its index
        }
    }
    return -1;               // not found
}
```

### How It Looks on an Array

Searching for `target = 7` in the array below:

```
 Index:    0   1   2   3   4   5   6   7
        +---+---+---+---+---+---+---+---+
        | 5 | 8 | 1 | 3 | 9 | 4 | 0 | 7 |
        +---+---+---+---+---+---+---+---+
          i → → → → → → → →   (walk until found)
```

| Step | `i` | `arr[i]` | Match? |
|------|-----|----------|--------|
| 1 | 0 | `5` | ❌ |
| 2 | 1 | `8` | ❌ |
| 3 | 2 | `1` | ❌ |
| 4 | 3 | `3` | ❌ |
| 5 | 4 | `9` | ❌ |
| 6 | 5 | `4` | ❌ |
| 7 | 6 | `0` | ❌ |
| 8 | 7 | `7` | ✅ → return `7` |

> 💡 Works on **any** array — sorted or not. Worst case: you check every element (`n` comparisons).

---

## 3. Binary Search

**Idea:** The array **must already be sorted**. Look at the middle element. If it's the target, done. If the target is smaller, search the **left half**; if larger, search the **right half**. Keep cutting in half until you find it (or run out of range).

```c
int BinarySearch(int arr[], int n, int target) {
    int l = 0, r = n - 1, m;
    while (l <= r) {
        m = l + (r - l) / 2;
        if (arr[m] == target) {
            return m;          // found
        } else if (target < arr[m]) {
            r = m - 1;         // search left half
        } else {
            l = m + 1;         // search right half
        }
    }
    return -1;                 // not found
}
```

### How It Looks on a Sorted Array

Searching for `target = 7` in this sorted array:

```
 Index:    0   1   2   3   4   5   6   7
        +---+---+---+---+---+---+---+---+
        | 1 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
        +---+---+---+---+---+---+---+---+
          l               m           r
```

| Step | `l` | `r` | `m` | `arr[m]` | Action |
|------|-----|-----|-----|----------|--------|
| 1 | `0` | `7` | `3` | `5` | `7 > 5` → search right → `l = 4` |
| 2 | `4` | `7` | `5` | `7` | ✅ found at index `5` |

> ⚠️ **Array must be sorted.**
>
> 💡 You can compute the midpoint either as `m = (l + r) / 2` or `m = l + (r - l) / 2` — both give the same result. If `l + r` could exceed the `int` limit (very large arrays), the second form is safer because it avoids overflow.

---

## 4. Selection Sort

**Idea:** Walk through the array. On each pass, find the **smallest** remaining element and **swap** it into the next position. After pass `i`, the first `i + 1` positions are sorted.

```c
void SelectionSort(int arr[], int n) {
    int minI, temp;
    for (int i = 0; i < n - 1; i++) {
        minI = i;                          // assume current is smallest
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minI]) {
                minI = j;                  // update index of smallest
            }
        }
        if (minI != i) {                   // swap only if needed
            temp = arr[i];
            arr[i] = arr[minI];
            arr[minI] = temp;
        }
    }
}
```

### Trace on `{2, 3, 4, 1, 9}`

```
Start:    [ 2,  3,  4,  1,  9 ]
```

| Pass `i` | Look at | Smallest Found | Swap Result |
|----------|---------|----------------|-------------|
| `0` | `2, 3, 4, 1, 9` | `1` at index `3` | `[1, 3, 4, 2, 9]` |
| `1` | `3, 4, 2, 9` | `2` at index `3` | `[1, 2, 4, 3, 9]` |
| `2` | `4, 3, 9` | `3` at index `3` | `[1, 2, 3, 4, 9]` |
| `3` | `4, 9` | `4` at index `3` | `[1, 2, 3, 4, 9]` (no swap) |

**Final:** `[1, 2, 3, 4, 9]` ✅

> 💡 Selection sort does **few swaps** (at most `n - 1` of them) — useful if swapping is expensive.

---

## 5. Bubble Sort

**Idea:** Walk through the array comparing **adjacent pairs**. If a pair is out of order, swap them. After each full pass, the largest remaining element "bubbles" to the end. Repeat until everything is in place.

```c
void BubbleSort(int arr[], int n) {
    int temp;
    for (int i = 0; i < n - 1; i++) {
        int swapped = 0;
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = 1;
            }
        }
        if (swapped == 0) break;     // early exit: array is already sorted
    }
}
```

> 💡 **Early exit:** If a full pass finishes without making **any** swap, the array is already sorted — we can stop immediately instead of doing the remaining passes. This makes bubble sort very fast on nearly-sorted data.

### Trace on `{5, 1, 4, 2, 8}` — Pass 1

```
Start:                [ 5,  1,  4,  2,  8 ]
Compare (5,1) → swap → [ 1,  5,  4,  2,  8 ]
Compare (5,4) → swap → [ 1,  4,  5,  2,  8 ]
Compare (5,2) → swap → [ 1,  4,  2,  5,  8 ]
Compare (5,8) → ok    → [ 1,  4,  2,  5,  8 ]
                                          ↑ largest "bubbled" to end
```

After all passes finish, the array becomes `[1, 2, 4, 5, 8]` ✅

> 💡 Why `j < n - i - 1`? Because after pass `i`, the last `i` elements are already in their final sorted positions — no need to compare them again.

---

## 🧪 Exercises

---

### Exercise 1: Linear Search

**Task:** Write a C program that takes an array and a target value, then uses **linear search** to find whether the target exists in the array. Print `FOUND` if it does, otherwise `NOT FOUND`.

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int LinearSearch(int arr[],int n,int target){
    for (int i = 0; i < n; i++)
    {
        if(arr[i]==target){
            return 1;
        }
    }
    return 0;
}

int main(){

    int n,target;
    int arr[10000];
    printf("Enter the size of the array: ");
    scanf("%d",&n);
    printf("Enter the elements of the array: ");
    for (int i = 0; i < n; i++)
    {
        scanf("%d",&arr[i]);
    }
    printf("Enter the target element you want to search for: ");
    scanf("%d",&target);
    if(LinearSearch(arr,n,target)==1)
        printf("FOUND\n");
    else
        printf("NOT FOUND\n");
    return 0;
}
```

**Sample run:**

```
Enter the size of the array: 5
Enter the elements of the array: 3 7 1 9 4
Enter the target element you want to search for: 9
FOUND
```

</details>

---

### Exercise 2: Binary Search

**Task:** Write a C program that takes a **sorted** array and a target value, then uses **binary search** to find the index of the target. Print the index if found, otherwise `NOT FOUND`.

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int BinarySearch(int arr[],int n,int target){
    int l=0,r=n-1,m;
    while (l<=r)
    {
        m=(l+r)/2; // m=l+(r-l)/2;
        if(arr[m]==target){
            return m;
        }
        else if(target<arr[m]){
            r=m-1;
        }
        else{ // target > arr[m]
            l=m+1;
        }
    }
    return -1;
}

int main(){

    int n,target;
    int arr[10000];
    printf("Enter the size of the array: ");
    scanf("%d",&n);
    printf("Enter the elements of the array: ");
    for (int i = 0; i < n; i++)
    {
        scanf("%d",&arr[i]);
    }
    printf("Enter the target element you want to search for: ");
    scanf("%d",&target);
    int result=BinarySearch(arr,n,target);
    if(result==-1){
        printf("NOT FOUND\n");
    }
    else{
        printf("FOUND in index %d\n",result);
    }
    return 0;
}
```

**Sample run:**

```
Enter the size of the array: 8
Enter the elements of the array (sorted): 1 3 4 5 6 7 8 9
Enter the target element you want to search for: 7
FOUND in index 5
```

> ⚠️ Binary search only works on a **sorted** array. If the input isn't sorted, the result is meaningless.

</details>

---

### Exercise 3: Selection Sort

**Task:** Write a C program that reads an array of integers and sorts it using **selection sort**, then prints the sorted result.

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

void SelectionSort(int arr[], int n){
    int minI,temp;
    for (int i = 0; i < n-1; i++)
    {
        minI=i;
        for (int j = i+1; j < n; j++)
        {
            if(arr[minI]>arr[j]){
                minI=j;
            }
        }
        if(minI!=i){
            temp=arr[i];
            arr[i]=arr[minI];
            arr[minI]=temp;
        }
    }
}

int main(){
    int n;
    int arr[10000];
    printf("Enter the size of the array: ");
    scanf("%d",&n);
    printf("Enter the elements of the array: ");
    for (int i = 0; i < n; i++)
    {
        scanf("%d",&arr[i]);
    }
    SelectionSort(arr,n);
    for (int i = 0; i < n; i++)
    {
        printf("%d ",arr[i]);
    }
    printf("\n");
    return 0;
}
```

**Sample run:**

```
Enter the size of the array: 5
Enter the elements of the array: 2 3 4 1 9
1 2 3 4 9
```

</details>

---

### Exercise 4: Bubble Sort

**Task:** Write a C program that reads an array of integers and sorts it using **bubble sort**, then prints the sorted result.

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

void BubbleSort(int arr[],int n){
    for (int i = 0; i < n-1; i++)
    {
        int temp;
        int swapped = 0;
        for (int j = 0; j < n-i-1; j++)
        {
            if(arr[j]>arr[j+1]){
                temp=arr[j];
                arr[j]=arr[j+1];
                arr[j+1]=temp;
                swapped = 1;
            }
        }
        if(swapped == 0) break;     // early exit: array is already sorted
    }
}
int main(){

    int n;
    int arr[10000];
    printf("Enter the size of the array: ");
    scanf("%d",&n);
    printf("Enter the elements of the array: ");
    for (int i = 0; i < n; i++)
    {
        scanf("%d",&arr[i]);
    }
    BubbleSort(arr,n);
    for (int i = 0; i < n; i++)
    {
        printf("%d ",arr[i]);
    }
    printf("\n");
    return 0;
}
```

**Sample run:**

```
Enter the size of the array: 5
Enter the elements of the array: 5 1 4 2 8
1 2 4 5 8
```

</details>

---

## 📋 Summary

<style>
.summary-table { width: 100%; border-collapse: collapse; table-layout: fixed; margin: 20px 0; }
.summary-table th, .summary-table td { border: 1px solid var(--border); padding: 6px 4px; vertical-align: top; width: 25%; }
.summary-table th { text-align: center; background: var(--accent-glow); border: 2px solid var(--accent); font-size: 0.85rem; font-family: var(--font-body); color: var(--accent); }
.summary-table .purpose { text-align: center; font-style: italic; font-size: 0.72rem; }
.summary-table .warn { color: var(--amber); font-style: normal; display: block; margin-top: 4px; font-size: 0.68rem; }
.summary-table pre { background: transparent; border: none; padding: 0; margin: 0; font-family: Consolas, "Courier New", monospace; font-size: 0.6rem; line-height: 1.4; white-space: pre; color: var(--text); overflow: hidden; font-variant-ligatures: none; font-feature-settings: "liga" 0, "calt" 0; }
.summary-table .visual pre { text-align: left; font-size: 0.62rem; }
.summary-table .when { background: var(--green-muted); font-size: 0.72rem; line-height: 1.4; }
@media (max-width: 600px) {
  .summary-table pre { font-size: 0.52rem; }
  .summary-table .visual pre { font-size: 0.54rem; }
  .summary-table .purpose, .summary-table .when { font-size: 0.65rem; }
}
</style>

<table class="summary-table">
  <thead>
    <tr>
      <th>Linear Search</th>
      <th>Binary Search</th>
      <th>Selection Sort</th>
      <th>Bubble Sort</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td class="purpose">Search for <code>x</code> in <code>arr</code></td>
      <td class="purpose">Search for <code>x</code> in <code>arr</code><span class="warn">⚠️ Must be sorted</span></td>
      <td class="purpose">Sort array <code>arr</code></td>
      <td class="purpose">Sort array <code>arr</code></td>
    </tr>
    <tr>
      <td class="visual"><pre>[5][8][1][3][9][4][0][7]
 0  1  2  3  4  5  6  7
 ↑
 i</pre></td>
      <td class="visual"><pre>[1][3][4][5][6][7][8][9]
 0  1  2  3  4  5  6  7
 ↑        ↑        ↑
 l        m        r</pre></td>
      <td class="visual"><pre>[2][3][4][1][9]
 0  1  2  3  4
 ↑        ↑
 i       minI</pre></td>
      <td class="visual"><pre>[2][3][4][1][9]
 0  1  2  3  4
 ↑  ↑
 j  j+1</pre></td>
    </tr>
    <tr>
      <td><pre>for(int i=0;i&lt;n;i++){
  if(arr[i]==x){
    return i;
  }
}</pre></td>
      <td><pre>while(l&lt;=r){
  int m=l+(r-l)/2;
  if(arr[m]==x)
    return m;
  if(arr[m]&lt;x)
    l=m+1;
  else
    r=m-1;
}
return -1;</pre></td>
      <td><pre>for(int i=0;i&lt;n-1;i++){
  minI=i;
  for(j=i+1;j&lt;n;j++){
    if(arr[j]&lt;arr[minI])
      minI=j;
  }
  if(minI!=i){
    temp=arr[minI];
    arr[minI]=arr[i];
    arr[i]=temp;
  }
}</pre></td>
      <td><pre>for(i=0;i&lt;n-1;i++){
  int swapped=0;
  for(j=0;j&lt;n-i-1;j++){
    if(arr[j]&gt;arr[j+1]){
      temp=arr[j];
      arr[j]=arr[j+1];
      arr[j+1]=temp;
      swapped=1;
    }
  }
  if(swapped==0) break;
}</pre></td>
    </tr>
    <tr>
      <td class="when"><strong>When to use:</strong><br>Small or unsorted arrays — when data isn't in order, or array is too small for sorting.</td>
      <td class="when"><strong>When to use:</strong><br>Large <strong>sorted</strong> arrays — far faster than linear; halves the range each step.</td>
      <td class="when"><strong>When to use:</strong><br>When sorting and you want to <strong>minimize swaps</strong> — performs at most <code>n−1</code> swaps total.</td>
      <td class="when"><strong>When to use:</strong><br>When sorting small or <strong>nearly-sorted</strong> arrays — simple and stable, and can early-exit when no swaps occur in a pass.</td>
    </tr>
  </tbody>
</table>

---

> ⬅️ [Back to Home](index.html)
