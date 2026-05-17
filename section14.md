---
layout: default
section_num: "14"
title: Structs in C
desc: Group related variables of different types into one unit using struct — declare, initialize, access members, and pass structs to functions.
tags: [struct, members, dot operator, user-defined types]
---

# 📘 Section 14 — Structs in C

 > A **struct** lets you bundle together several variables — possibly of **different types** — into a single named unit. Instead of carrying around 5 separate variables for a student, you carry one `struct Student`.

---

## 🎯 What You'll Practice

- Declaring a `struct` and listing its members
- Creating struct variables and initializing them at declaration
- Accessing members using the dot operator (`.`)
- Copying one struct into another with simple assignment
- Passing structs to functions and returning values from them
- Working with **arrays of structs**

---

## 1. Why Do We Need Structs?

Imagine you want to store data about a student: their **GPA**, their **letter grade**, their **age**, their **name**. Using normal variables, you'd write:

```c
float gpa;
char grade;
int age;
char name[50];
```

That works for **one** student. For 100 students, you'd need 100 of each — and nothing ties them together. A **struct** solves this by bundling related fields into a single type you can reuse.

---

## 2. Declaring a Struct

```c
#include <stdio.h>

struct student {
    float gpa;
    char grade;
};
```

This **defines** a new type called `struct student`. No memory is reserved yet — we've only described what a `student` looks like. To actually create one, we declare a **variable** of that type.

---

## 3. Creating and Using a Struct

```c
#include <stdio.h>

struct student {
    float gpa;
    char grade;
};

int main() {
    struct student s1;        // declaration — like "int s1;" but for our new type

    s1.gpa = 3.9;             // access members with the dot operator
    s1.grade = 'A';

    printf("GPA: %.2f, GRADE: %c\n", s1.gpa, s1.grade);
    return 0;
}
```

**Output:**

```
GPA: 3.90, GRADE: A
```

> 💡 The **dot operator `.`** reads as *"of"* — so `s1.gpa` reads as *"the gpa of s1"*.

---

## 4. Initializing a Struct at Declaration

You can fill in all the members the moment you create the variable, using curly braces:

```c
struct student s1 = {3.9, 'A'};        // gpa = 3.9, grade = 'A'
```

The values are matched **in order** to the members listed in the struct definition.

```c
#include <stdio.h>

struct student {
    float gpa;
    char grade;
};

int main() {
    struct student s1 = {3.9, 'A'};
    printf("GPA: %.2f, GRADE: %c\n", s1.gpa, s1.grade);
    return 0;
}
```

---

## 5. Copying a Struct

You can copy **all** the members of one struct into another with a single assignment — C handles each field for you:

```c
#include <stdio.h>

struct student {
    float gpa;
    char grade;
};

int main() {
    struct student s1 = {3.9, 'A'};
    struct student s2;

    s2 = s1;        // copies every member of s1 into s2

    printf("GPA: %.2f, GRADE: %c\n", s2.gpa, s2.grade);
    return 0;
}
```

> 💡 Struct **assignment** copies all members at once. This is one of the few cases where C lets you "assign" a whole block of data with `=`.

---

## 6. Arrays of Structs

To store many students, declare an array of structs:

```c
struct student students[2];        // 2 students

students[0].gpa = 3.9;
students[0].grade = 'A';

students[1].gpa = 2.7;
students[1].grade = 'C';
```

Each element of the array is a complete `struct student` — with all its fields.

---

## 7. Reading Strings into a Struct Member — A Common Pitfall

When a struct contains a `char name[50]` and you mix `fgets` with `scanf`, you'll usually hit a small annoyance: `fgets` reads the leftover `\n` from the previous `scanf`, or it keeps the trailing `\n` in your string.

```c
printf("Enter student name: ");
fgets(students[i].name, sizeof(students[i].name), stdin);
students[i].name[strlen(students[i].name) - 1] = '\0';   // strip the trailing '\n'

printf("Enter student age: ");
scanf("%d", &students[i].age);

printf("Enter total marks: ");
scanf("%f", &students[i].totalMarks);
fflush(stdin);     // clear the leftover '\n' so the next fgets isn't skipped
```

> ⚠️ `fflush(stdin)` is **undefined behavior** in standard C, but on most compilers (like the ones used for MS Windows) it works as expected — it clears the input buffer.

---

## 🧪 Exercises

---

### Exercise 1: Student Records

**Task:** Create a structure called `Student` with members `name`, `age`, and `totalMarks`. Write a C program to:

1. Input data for **two** students.
2. Display each student's information.
3. Calculate and print the **average** of their total marks.

<details markdown="1">
<summary>💡 Hint</summary>

- Define the struct with three members: `char name[50]`, `int age`, `float totalMarks`.
- Use an **array** of `struct Student` of size `2`.
- Read names with `fgets` (so spaces are allowed), then strip the trailing `'\n'`.
- Sum both `totalMarks` and divide by `2.0` to get the average.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>
#include <string.h>

struct Student
{
    char name[50];
    int age;
    float totalMarks;
};

void displayStudentData(struct Student s)
{
    printf("\nStudent Data:\n");
    printf("Name: %s\n", s.name);
    printf("Age: %d\n", s.age);
    printf("Total Marks: %.2f\n", s.totalMarks);
}

int main()
{
    struct Student students[2];
    double sumOfAllMarks = 0;
    for (int i = 0; i < 2; i++)
    {
        printf("\nEnter student %d data:\n", i + 1);

        printf("Enter student name: ");
        fgets(students[i].name, sizeof(students[i].name), stdin);
        students[i].name[strlen(students[i].name) - 1] = '\0'; // remove the \n which is read by fgets after the user enters the string and press enter

        printf("Enter student age: ");
        scanf("%d", &students[i].age);

        printf("Enter total marks: ");
        scanf("%f", &students[i].totalMarks);
        fflush(stdin); // very important! empty the buffer so the already read \n (when you enter the input and press enter) don't be read by the next fgets
    }
    for (int i = 0; i < 2; i++)
    {
        displayStudentData(students[i]);
        sumOfAllMarks = sumOfAllMarks + students[i].totalMarks;
    }
    double averageMarks = sumOfAllMarks / 2;
    printf("--------\nAverage of marks: %.2f\n", averageMarks);
    return 0;
}
```

**Sample run:**

```
Enter student 1 data:
Enter student name: Ahmed
Enter student age: 20
Enter total marks: 85.5

Enter student 2 data:
Enter student name: Mona
Enter student age: 21
Enter total marks: 92.0

Student Data:
Name: Ahmed
Age: 20
Total Marks: 85.50

Student Data:
Name: Mona
Age: 21
Total Marks: 92.00
--------
Average of marks: 88.75
```

</details>

---

### Exercise 2: Circles

**Task:** Define a structure named `Circle` with one member, `radius`. Write a C program to:

1. Input the radius for **two** circles.
2. Calculate the **area** and **perimeter** of each.
3. Display the results.

Use the formulas:

| Quantity | Formula |
|----------|---------|
| Area | `π × radius × radius` |
| Perimeter | `2 × π × radius` |

For `π`, use `22 / 7.0` (or `3.14159`).

<details markdown="1">
<summary>💡 Hint</summary>

- Define `struct Circle` with one `double radius` member.
- Write two functions: `calculateArea(struct Circle c)` and `calculatePerimeter(struct Circle c)`.
- ⚠️ Use `22 / 7.0` (not `22 / 7`), otherwise C does integer division and gives `3` instead of `~3.14`.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

struct Circle
{
    double radius;
};

double calculateArea(struct Circle c)
{
    return 22 / 7.0 * c.radius * c.radius;
}

double calculatePerimeter(struct Circle c)
{
    return 2 * 22 / 7.0 * c.radius;
}

int main()
{
    struct Circle circles[2];

    for (int i = 0; i < 2; i++)
    {
        printf("\nEnter circle %d radius: ", i + 1);
        scanf("%lf", &circles[i].radius);
    }

    for (int i = 0; i < 2; i++)
    {
        double area = calculateArea(circles[i]);
        double perimeter = calculatePerimeter(circles[i]);

        printf("\nCircle %d:\n", i + 1);
        printf("Radius: %.2f\n", circles[i].radius);
        printf("Area: %.2f\n", area);
        printf("Perimeter: %.2f\n", perimeter);
    }

    return 0;
}
```

**Sample run:**

```
Enter circle 1 radius: 7
Enter circle 2 radius: 3.5

Circle 1:
Radius: 7.00
Area: 154.00
Perimeter: 44.00

Circle 2:
Radius: 3.50
Area: 38.50
Perimeter: 22.00
```

</details>

---

### Exercise 3: Employees & Highest Salary

**Task:** Create a structure called `Employee` to store `id`, `name`, and `salary`. Write a program to:

1. Input data for **three** employees.
2. Display the details of all three.
3. Find and print the employee with the **highest salary**.

<details markdown="1">
<summary>💡 Hint</summary>

- Define `struct Employee` with `int id`, `char name[50]`, `double salary`.
- While reading input, keep track of an `highestSalaryIndex` variable. After each new employee, compare their salary to `employees[highestSalaryIndex].salary` and update if larger.
- After all input is read, the variable points to the highest-paid employee.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>
#include <string.h>

struct Employee
{
    int id;
    char name[50];
    double salary;
};

int main()
{
    struct Employee employees[3];
    int highestSalaryIndex = 0;

    for (int i = 0; i < 3; i++)
    {
        printf("\nEnter employee %d details:\n", i + 1);
        printf("Employee ID: ");
        scanf("%d", &employees[i].id);
        fflush(stdin);
        printf("Name: ");
        fgets(employees[i].name, sizeof(employees[i].name), stdin);
        employees[i].name[strlen(employees[i].name) - 1] = '\0';
        printf("Salary: ");
        scanf("%lf", &employees[i].salary);

        if (employees[i].salary > employees[highestSalaryIndex].salary)
        {
            highestSalaryIndex = i;
        }
    }

    printf("\nDetails of all employees:\n");
    for (int i = 0; i < 3; i++)
    {
        printf("\nEmployee %d:\n", i + 1);
        printf("Employee ID: %d\n", employees[i].id);
        printf("Name: %s\n", employees[i].name);
        printf("Salary: %.2f\n", employees[i].salary);
    }

    printf("\nEmployee with the highest salary:\n");
    printf("Employee ID: %d\n", employees[highestSalaryIndex].id);
    printf("Name: %s\n", employees[highestSalaryIndex].name);
    printf("Salary: %.2f\n", employees[highestSalaryIndex].salary);

    return 0;
}
```

**Why track the index, not the salary?**
By saving the **index**, we keep a reference to the **full record** (id, name, and salary) — not just the salary number. That way we can print all three fields at the end without searching the array again.

</details>

---

## 📋 Quick Reference

| Concept | Syntax |
|---------|--------|
| Define a struct | `struct Name { type member1; type member2; };` |
| Declare a variable | `struct Name v;` |
| Initialize at declaration | `struct Name v = {value1, value2};` |
| Access a member | `v.member` |
| Copy whole struct | `v2 = v1;` |
| Array of structs | `struct Name arr[10];` then `arr[i].member` |
| Pass to a function | `void f(struct Name s)` called with `f(v);` |

---

> ⬅️ [Back to Home](index.html)
