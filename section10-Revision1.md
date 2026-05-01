---
layout: default
section_num: "10 Revision 01"
title: Revision Sheet 1
desc: Mixed revision problems covering arrays, loops, functions, matrices, and classic algorithmic patterns.
tags: [arrays, loops, functions, matrices, revision]
---

# 📘 Revision — Sheet 1

 > A full revision sheet mixing everything you've learned so far: arrays, nested loops, functions, pointers-style thinking, and 2D matrices. Try every problem on your own first, then peek at the solution.

---

## 🎯 What You'll Practice

- Nested loops and pattern printing
- Writing and calling your own functions
- Digit-by-digit number manipulation (`%10`, `/10`)
- 2D matrices: scan, print, add, subtract, multiply, transpose
- Classic problems: Fibonacci, GCD, Strong numbers, Pythagorean triples

---

## 🧪 Exercises

---

### Exercise 1: Print Unique Numbers (No Duplicates)

**Task:** Use a single-subscripted array to solve the following problem. Read in 20 numbers, each of which is between 10 and 100 inclusive. As each number is read, print it only if it's not a duplicate of a number already read. Provide for the "worst case" in which all 20 numbers are different. Use the smallest possible array to solve this problem.

<details markdown="1">
<summary>💡 Hint</summary>

- Keep an array to store numbers you've already seen, and a variable `index` that tracks how many unique numbers you've stored so far
- For each new number, use a `flag` variable set to `0`, then loop through the stored numbers and set `flag = 1` if you find a duplicate
- If `flag` is still `0` after the inner loop, the number is unique → print it and add it to the array
- The "smallest possible array" is of size 20 (worst case: all numbers different)

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){

    int arr[20]; //[1,2,3]
    int index=0;
    int num;
    int flag;

    for (int i = 0; i < 20; i++)
    {
        scanf("%d",&num);
        flag=0;
        for (int j = 0; j < index; j++)
        {
            if (num==arr[j])
            {
                flag=1;
            }  
        }
        if (flag==0)
        {
            printf("%d ",num);
            arr[index]=num;
            index++;
        }        
    }
    return 0;
}
```

</details>

---

### Exercise 2: Sum of Numbers by Digit Sum Range

**Task:** Given three numbers N, A, B. Print the summation of the numbers between 1 and N whose sum of digits is between A and B inclusive.

<details markdown="1">
<summary>💡 Hint</summary>

- Write a helper function `sumOfDigits(num)` that repeatedly does `num % 10` to grab the last digit, adds it to a running sum, then does `num / 10` to drop that digit
- Loop from `1` to `N`, call `sumOfDigits(i)` on each number, and if the result is between `A` and `B` inclusive, add `i` to the total
- Be careful: you're adding `i` to the total, not the sum of its digits

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int sumOfDigits(int num){ 
    int sum=0;
    while (num!=0)
    {
        sum=sum+num%10;
        num=num/10;
    }
    return sum;  
}

int main(){

    int N,A,B,sum=0,sOfDigits;
    scanf("%d",&N);
    scanf("%d",&A);
    scanf("%d",&B);
    for (int i = 1; i <= N; i++)
    {
        sOfDigits = sumOfDigits(i);
        if(sOfDigits>=A && sOfDigits<=B){
            sum+=i;
        }
    }
    printf("%d",sum);
    return 0;
}
```

</details>

---

### Exercise 3: Repeat a Symbol

**Task:** Given 3 lines of input described as follows:
- First line contains a symbol `S` (`*`, `/`, `+`, `-`).
- Second line contains a number `N`.
- Third line contains `N` numbers.

For each number `Xi` in the N numbers, print a new line that contains the symbol `S` repeated `Xi` times.

<details markdown="1">
<summary>💡 Hint</summary>

- Use `scanf("%c", &c)` to read the character
- Use a nested loop: outer loop runs `N` times (once per number), inner loop runs `x` times and prints the character
- Don't forget `\n` after each inner loop finishes

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){

    char c;
    int N,x;
    scanf("%c",&c);
    scanf("%d",&N);
    for (int i = 0; i < N; i++)
    {
        scanf("%d",&x);
        for (int j = 0; j < x; j++)
        {
            printf("%c",c);
        }
        printf("\n");  
    }
    
    return 0;
}
```

</details>

---

### Exercise 4: Lucky Array

**Task:** Given a number `N` and an array `A` of `N` numbers. Determine if the array is lucky or not.

> **Note:** The array is lucky if the frequency (number of occurrences) of the minimum element is **odd**.

**Examples:**

```example
[2,2,1,1,1] --> LUCKY       (min=1, appears 3 times, odd)
[6,6,7,6]   --> LUCKY       (min=6, appears 3 times, odd)
[1,2,3,4,1] --> NOT LUCKY   (min=1, appears 2 times, even)
[2,2,2,4,5] --> LUCKY       (min=2, appears 3 times, odd)
```

<details markdown="1">
<summary>💡 Hint</summary>

- Break the problem into 3 steps:
  1. Find the minimum in the array (loop and compare)
  2. Count how many times the minimum appears (another loop)
  3. Check if the count is odd (`count % 2 != 0`) → LUCKY, otherwise NOT LUCKY

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){

    // input: N, A[N]
    // steps:
    // 1. search for minimmum number "done"
    // 2. find frequency of the minimum number  "done"
    // 3. frequency is odd (lucky) or even (not lucky)? 
    // output: lucky or not lucky
    // EXAMPLES:
    // [2,2,1,1,1] --> lucky
    // [6,6,7,6]   --> lucky
    // [1,2,3,4,1] --> not lucky
    // [2,2,2,4,5] --> lucky

    int N;
    scanf("%d",&N);
    int A[N];
    for (int i = 0; i < N; i++)
    {
        scanf("%d",&A[i]);
    }
    int min=A[0];
    for (int i = 0; i < N; i++)
    {
        if (min>A[i]){
            min=A[i];
        } 
    }
    int c=0;
    for (int i = 0; i < N; i++)
    {
        if (min==A[i]){
            c++;
        } 
    }
    if (c%2==0)
    {
        printf("NOT LUCKY");
    }
    else
    {
        printf("LUCKY");
    }
    
    return 0;
}
```

</details>

---

### Exercise 5: Swap Min and Max in Array

**Task:** Given a number `N` and an array `A` of `N` numbers. Print the array after doing the following operations:
- Find the minimum number in these numbers.
- Find the maximum number in these numbers.
- Swap the minimum number with the maximum number.

<details markdown="1">
<summary>💡 Hint</summary>

- Don't just track the min/max **values** — also track their **indices** (`minIndex`, `maxIndex`), because you need the indices to swap
- Classic swap with a temp variable: `temp = A[minIndex]; A[minIndex] = A[maxIndex]; A[maxIndex] = temp;`
- Then just print the array after the swap

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){

    int N;
    scanf("%d",&N);
    int A[N];
    for (int i = 0; i < N; i++)
    {
        scanf("%d",&A[i]);
    }
    int min=A[0], minIndex=0;
    for (int i = 0; i < N; i++)
    {
        if (min>A[i])
        {
            min=A[i];
            minIndex=i;
        } 
    }
    int max=A[0], maxIndex=0;
    for (int i = 0; i < N; i++)
    {
        if (max<A[i])
        {
            max=A[i];
            maxIndex=i;
        } 
    }

    // [1,2,3,5,4]
    //  0,1,2,3,4   <-- index
    int temp=A[minIndex]; // 1
    A[minIndex]  = A[maxIndex];
    A[maxIndex]  = temp;

    for (int i = 0; i < N; i++)
    {
        printf("%d ",A[i]);
    }
    return 0;
}
```

</details>

---

### Exercise 6: First 10 Fibonacci Numbers

**Task:** Write a C program to find and print the first 10 Fibonacci numbers using functions.

<details markdown="1">
<summary>💡 Hint</summary>

- Fibonacci sequence: `0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...` — each number is the sum of the two before it
- Start with `n1 = 0` and `n2 = 1`, print them first
- In a loop, calculate `n3 = n1 + n2`, print `n3`, then **shift**: `n1 = n2; n2 = n3;`
- Loop 8 more times to get 10 total numbers (since you already printed 2)

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){

    // 0  1  1  2 3 5 8 13 21
    // n1 n2 n3
 
    int n1=0, n2=1,n3;
    printf("%d %d ",n1,n2);
    // n3=n1+n2; then print n3
    // n1=1 n2=1
    // n3=1+1=2  then print n3
    // n1=1 n2=2
    // n3=1+2=3  then print n3
    for (int i = 0; i < 8; i++)
    {
        n3=n1+n2;
        printf("%d ",n3);
        n1=n2;
        n2=n3;
    }
    return 0;
}
```

</details>

---

### Exercise 7: Strong Number

**Task:** Write a program to check whether a given number is a strong number or not.

> **Example:** `1! + 4! + 5! = 1 + 24 + 120 = 145` → `145` is a strong number.

<details markdown="1">
<summary>💡 Hint</summary>

- Write a `fact(num)` function that returns the factorial using a `while` loop
- Keep the original number in a variable (e.g. `num`) and a copy (e.g. `n`) to modify
- Extract each digit with `n % 10`, compute `fact()` of that digit, add to `sum`, then `n = n / 10`
- At the end compare `num` (original) with `sum` — equal → STRONG, otherwise NOT STRONG

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int fact(int num){ 
    int f=1;
    while (num!=0)
    {
        f=f*num;
        num--;
    }
    return f;
}

int main(){

    // 6!=6*5*4*3*2*1
    // 145 , 1!=1, 4!=4*3*2*1=24 , 5!=5*4*3*2*1=120
    // 120+24+1= 145

    // input: num
    // steps:
    // 1. bring each digit
    // 2. bring the factorial of each digit from step 1
    // 3. calculate the sum of the factorial calculated in step 2
    // 4. if (num==sum) --> strong else --> not strong
    //output: strong or not strong

    int num, sum=0;
    scanf("%d",&num);
    int n= num;

    while (n!=0)
    {
        sum=sum+fact(n%10);
        n=n/10;
    }
    if (num==sum){
        printf("STRONG");
    }
    else{
        printf("NOT STRONG");
    }
    return 0;
}
```

</details>

---

### Exercise 8: GCD (Greatest Common Divisor)

**Task:** Write a program to find the GCD (greatest common divisor) of two numbers.

<details markdown="1">
<summary>💡 Hint</summary>

- The GCD of `a` and `b` is the largest number that divides **both** of them with no remainder
- Loop `i` from `2` up to the smaller of `a` and `b`
- If both `a % i == 0` and `b % i == 0`, update `gcd = i`
- At the end, `gcd` holds the largest common divisor (initialize it to `1`, since 1 always divides anything)

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){
    //a=12 b=24
    int a,b,gcd=1;
    scanf("%d %d",&a,&b);

    for (int i = 2; i <=a && i<=b ; i++)
    {
        if (a%i==0 && b%i==0)
        {
            gcd=i;
        }
    }
    printf("%d",gcd);
    return 0;
}
```

</details>

---

### Exercise 9: Volume of a Cylinder

**Task:** Write a program to calculate the volume of a cylinder using user input. Read from the user the radius and height and output the volume. Consider π = 3.14.

> **Formula:** `volume = π × radius² × height`

<details markdown="1">
<summary>💡 Hint</summary>

- Use `double` (with `%lf` in `scanf`) for the radius and height so fractional values work
- `r*r` is squaring — no need for a `pow` function
- Use `%f` in `printf` for the output

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){

    double r,h,v;
    scanf("%lf%lf",&r,&h);
    v=3.14*r*r*h;
    printf("v = %f",v);
    return 0;
}
```

</details>

---

### Exercise 10: Print All Factors of a Number

**Task:** Write a C program to find all factors of a number.

<details markdown="1">
<summary>💡 Hint</summary>

- A **factor** of `n` is any number `i` such that `n % i == 0`
- Loop `i` from `1` to `n` inclusive; every time `n % i == 0`, print `i`
- Factors of `12`: `1 2 3 4 6 12`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){

    int n;
    scanf("%d",&n);

    for ( int i = 1; i <= n; i++)
    {
        if (n%i==0)
        {
            printf("%d ",i);
        }   
    }
    return 0;
}
```

</details>

---

### Exercise 11: Search Function

**Task:** Write a function that searches for a specific integer in an array and returns `1` if it is found and `0` if not.

<details markdown="1">
<summary>💡 Hint</summary>

- Function signature: `int search(int arr[], int size, int n)`
- Loop through the array — the moment you find `arr[i] == n`, `return 1` immediately (no need to keep looping)
- If the loop finishes without finding it, `return 0` after the loop
- `sizeof(arr)/sizeof(arr[0])` gives the number of elements of an array declared in the same scope

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int search(int arr[], int size, int n){
    for (int i = 0; i < size; i++)
    {
        if (arr[i]==n)
        {
            return 1;
        }
    }
    return 0;
}

int main(){

    int arr[]={1,2,3,4,5,6,1,20};
    int size=sizeof(arr)/sizeof(arr[0]);
    int n=4;

    if (search(arr,size,n)==1)
    {
        printf("FOUND");
    }
    else{
        printf("NOT FOUND");
    }
    return 0;
}
```

</details>

---

### Exercise 12: Series 1 + 11 + 111 + 1111 + ...

**Task:** Write a program in C to find the sum of the series `1 + 11 + 111 + 1111 + ...` up to `n` terms.

**Test Data:**

```example
Input the number of terms : 5

Expected Output :
1 + 11 + 111 + 1111 + 11111
The Sum is : 12345
```

<details markdown="1">
<summary>💡 Hint</summary>

- Start with `p = 1` (the first term). To get the next term: `p = p * 10 + 1` → `1 → 11 → 111 → 1111 ...`
- Keep a running `sum += p` inside the loop
- For the pretty output, print `p+` for every term **except** the last one; for the last term (`i == n-1`), print just `p` without the `+`

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){

    int n,sum=0,p=1;
    scanf("%d",&n);
    // 123 % 10 = 3
    // 123 / 10 = 12  // integer division
    // 123 * 10 = 1230

    // 1 + 11 + 111 + 1111
    for (int i = 0; i < n; i++)
    {
        sum= sum+p;
        if (i==n-1)
        {
            printf("%d",p);
        }
        else{
            printf("%d+",p);
        }
        p=p*10 +1;
    }
    printf("\nSum = %d",sum);
    return 0;
}
```

</details>

---

### Exercise 13: Number Triangle Pattern

**Task:** Write a C program to display a pattern like a right angle triangle with numbers.

**The pattern:**

```
1
12
123
1234
```

<details markdown="1">
<summary>💡 Hint</summary>

- Classic nested loop — outer loop for rows, inner loop for columns
- On row `i` (0-indexed), print numbers from `1` to `i+1`
- In the inner loop print `j+1` (since `j` starts at `0`), and `\n` after the inner loop

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){

    int n;
    scanf("%d",&n);

    for (int i = 0; i < n; i++) // rows
    {
        for (int j = 0; j <= i; j++) // cols
        {
            printf("%d",j+1);
        }
        printf("\n");
    }
    return 0;
}
```

</details>

---

### Exercise 14: Multiplication Table 6–10

**Task:** Write a C program that prints the following output:

```
         6  7  8  9  10
6 	36 42 48 54  60
7 	42 49 56 63  70
8 	48 56 64 72  80
9 	54 63 72 81  90
10	 60 70 80 90 100
```

<details markdown="1">
<summary>💡 Hint</summary>

- Print the header row manually with `\t` (tab) before `6 7 8 9 10`
- Then loop `i` from `6` to `10`, and for each row print `i` followed by `i*6, i*7, i*8, i*9, i*10`
- Use `\t` to line up the columns

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){

    printf("\t6  7  8  9  10\n");
    for(int i=6;i<=10;i++)
    {
        printf("%d\t%d %d %d %d %d\n",i,i*6,i*7,i*8,i*9,i*10);
    }
    return 0;
}
```

</details>

---

### Exercise 15: Print Unique Elements in an Array

**Task:** Write a program in C to print all unique elements in an array.

> A unique element is one that appears **exactly once** in the array. Example: in `{1,2,3,4,5,4,3}` the unique elements are `1 2 5`.

<details markdown="1">
<summary>💡 Hint</summary>

- Use a nested loop: outer loop picks `arr[i]`, inner loop counts how many times `arr[i]` appears in the whole array
- If `count == 1` at the end of the inner loop, print `arr[i]`
- Note this is different from Exercise 1 — here we print only truly unique elements, not the first occurrence of each

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){
    // {1,2,3,4,5,4,3};
    // 1 2 5
    int  n,count;
    scanf("%d",&n);
    int arr[n];
    for (int i = 0; i < n; i++)
    {
        scanf("%d",&arr[i]);
    }

    for (int i = 0; i < n; i++)
    {
        count=0;
        for (int j = 0; j < n; j++)
        {
            if(arr[i]==arr[j]){
                count++;
            }
        }
        if (count==1)
        {
            printf("%d ",arr[i]);
        }        
    }
    return 0;
}
```

</details>

---

### Exercise 16: Matrix Calculator (3×3)

**Task:** Write a program that accepts two (3 × 3) matrices from the user and then asks the user to select one operation:
- Multiplication
- Addition
- Subtraction
- Transpose

The program should print the output as a (3 × 3) matrix.

<details markdown="1">
<summary>💡 Hint</summary>

- Break the program into **helper functions**: `scanMatrix`, `printMatrix`, `addMatrix`, `subMatrix`, `multMatrix`, `transposeMatrix` — much cleaner than one giant `main`
- Add/Sub: `r[i][j] = m1[i][j] ± m2[i][j]`
- Transpose: `r[i][j] = m1[j][i]` (swap row and column)
- Multiplication uses **three** nested loops: `r[i][j] = sum of m1[i][z] * m2[z][j]` for `z` from 0 to 2 — don't forget to reset `r[i][j] = 0` before that inner sum
- Use `switch` on the user's choice to call the right function

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
void scanMatrix(int arr[3][3]){
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            scanf("%d",&arr[i][j]);
        }
    }
}
void printMatrix(int arr[3][3]){
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            printf("%d ",arr[i][j]);
        }
        printf("\n");
    }
}
void addMatrix(int m1[3][3],int m2[3][3],int r[3][3]){
    for (int i = 0; i < 3; i++) // rows
    {
        for (int j = 0; j < 3; j++) //cols
        {
            r[i][j]=m1[i][j]+m2[i][j];
        }
    }
}
void subMatrix(int m1[3][3],int m2[3][3],int r[3][3]){
    for (int i = 0; i < 3; i++) // rows
    {
        for (int j = 0; j < 3; j++) //cols
        {
            r[i][j]=m1[i][j]-m2[i][j];
        }
    }
}
void transposeMatrix(int m1[3][3],int r[3][3]){
    for (int i = 0; i < 3; i++) // rows
    {
        for (int j = 0; j < 3; j++) //cols
        {
            r[i][j]=m1[j][i];
        }
    }
}
void multMatrix(int m1[3][3], int m2[3][3],int r[3][3]){
    for (int i = 0; i < 3; i++) // rows
    {
        for (int j = 0; j < 3; j++) //cols
        {
            r[i][j]=0;
            for (int z = 0; z < 3; z++)
            {
                r[i][j]=r[i][j]+m1[i][z] * m2[z][j];
            }
            
        }
    }
}

int main(){
    //   0 1 2
    // 0{1,2,3}  {1,1,1} = {2,3,4}   1*1+2*2+3*3=14                   1-->0,0   2-->0,1  3-->0,2     1-->0,0   2-->1,0  3-->2,0
    // 1{1,2,3}  {2,2,2} = {3,4,5}
    // 2{1,2,3}  {3,3,3} = {4,5,6}
    //    m1       m2   =    r


    int m1[3][3];
    int m2[3][3];
    int r[3][3];
    int n;
    printf("For add press 1\n");
    printf("For sub press 2\n");
    printf("For mul press 3\n");
    printf("For transpose press 4\n");
    scanf("%d",&n); //2
    switch (n)
    {
    case 1:
        scanMatrix(m1);
        scanMatrix(m2);
        addMatrix(m1,m2,r);
        printMatrix(r);
        break;
    case 2:
        scanMatrix(m1);
        scanMatrix(m2);
        subMatrix(m1,m2,r);
        printMatrix(r);
        break;
    case 3:
        scanMatrix(m1);
        scanMatrix(m2);
        multMatrix(m1,m2,r);
        printMatrix(r);
        break;
    case 4:
        scanMatrix(m1);
        transposeMatrix(m1,r);
        printMatrix(r);
        break;
    default:
        printf("ERROR CHOICE!");
        break;
    }
    return 0;
}
```

</details>

---

### Exercise 17: Pythagorean Triples

**Task:** A right triangle can have sides that are all integers. The set of three integer values for the sides of a right triangle is called a **Pythagorean triple**. These three sides must satisfy the relationship that the sum of the squares of two of the sides is equal to the square of the hypotenuse. Write a program to find all Pythagorean triples for `side1`, `side2`, and the `hypotenuse` all no larger than 30. Use a triple-nested `for` loop that simply tries all possibilities.

<details markdown="1">
<summary>💡 Hint</summary>

- Relationship: `hyp² = side1² + side2²`
- Three nested loops: `i`, `j`, `k` each going from `1` to `30`
- Inside the innermost loop check `if (k*k == i*i + j*j)` then print the triple
- Total iterations: `30 × 30 × 30 = 27000` — brute force, but it works

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
// 3 3 6
// h = root(x^2 + y^2)
// h^2=x^2+y^2
// 18 =3^2 +3^2;
// 1 30
// 1 1 1
// 1 1 2
// 1 1 3
// .
// .
// 1 1 30
// 1 2 1
// 1 2 2

#include <math.h>
int main(){
    for (int i = 1; i <= 30; i++) // loop of side1
    {
        for (int j = 1; j <= 30; j++) // loop of side2
        {
            for (int k = 1; k <= 30; k++) // loop of hypotnous
            {
                if (k*k==(i*i)+(j*j))
                {
                    printf("s1:%d s2:%d hyp:%d is pythegorean triples\n",i,j,k);
                }        
            } 
        } 
    }   
    // number of total loops = 30 * 30 * 30 = 27000
    return 0;
}
```

</details>

---

### Exercise 18: Maximum Element of Each Row

**Task:** Find the maximum element of each row in a matrix.

<details markdown="1">
<summary>💡 Hint</summary>

- For each row, **reset** `max` to `arr[i][0]` at the start of that row — don't reuse the old row's max!
- Then loop through the columns of that row comparing against `max`
- Print the max after each row's inner loop finishes (not after the whole matrix)

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){

    int arr[3][5]=
    {
        {10,2,3,4,4},
        {1,2,1,3,3},
        {3,2,5,7,8}
    };

    for (int i = 0; i < 3; i++) // rows
    {
        int max=arr[i][0];
        for (int j = 0; j < 5; j++) // cols
        {
            if (arr[i][j]>max)
            {
                max=arr[i][j];
            } 
        }
        printf("Max element in row number %d equal %d\n",i+1,max);
    }
    return 0;
}
```

</details>

---

### Exercise 19: Sum of All Elements in a 4×3 Matrix

**Task:** Write a program that initializes a 4×3 matrix of integers with predetermined values and then computes the sum of all elements in the matrix.

<details markdown="1">
<summary>💡 Hint</summary>

- Initialize the 4×3 matrix directly in the declaration using nested `{}` braces
- Classic nested loop: outer loop over 4 rows, inner loop over 3 columns
- Keep a single `sum` variable and add `arr[i][j]` each iteration

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
int main(){
    
    int arr[4][3]=
    {
        {1,2,2},
        {1,2,1},
        {3,2,5},
        {3,2,5}
    };
    int sum=0;
    for (int i = 0; i < 4; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            sum=sum+arr[i][j];
        } 
    }
    printf("sum= %d",sum);
    
    return 0;
}
```

</details>

---

### Exercise 20: Check If Two Matrices Are Equal

**Task:** Write a C program that checks if 2 matrices are equal or not.

<details markdown="1">
<summary>💡 Hint</summary>

- Two matrices are equal **only** if **every** corresponding element is the same
- Write an `isEqualMatrix` function — loop through both matrices, and the moment you find **any** mismatch, `return 0` immediately (early exit)
- If the whole loop finishes without a mismatch, `return 1`
- In `main`, call the function and print the result based on the return value

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
void scanMatrix(int m1[3][3]){
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            scanf("%d",&m1[i][j]);
        }
    }
}

int isEqualMatrix(int m1[3][3], int m2[3][3]){
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            if (m1[i][j]!=m2[i][j])
            {
                return 0;
            }  
        }
    }
    return 1;
}

int main(){

    int m1[3][3];
    int m2[3][3];
    scanMatrix(m1);
    scanMatrix(m2);

    if(isEqualMatrix(m1,m2)==1){
        printf("EQUAL MATRIX");
    }
    else
    {
        printf("NOT EQUAL MATRIX");
    }
    

    return 0;
}
```

</details>

---

> ⬅️ [Back to Home](index.html)
