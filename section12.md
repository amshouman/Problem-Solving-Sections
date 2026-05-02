---
layout: default
section_num: "12"
title: Strings
desc: Introduction to strings, how they are stored in memory, common string library functions, and exercises on length, concatenation, reversal, character counting
tags: [strings, char arrays, strlen, strcat, strcpy, null terminator]
---

# 📘 Section 12 — Strings in C

 > A string in C is just an **array of characters** that ends with a special character `'\0'` (the null terminator). That `'\0'` is what tells C *"the string ends here."*

---

## 🎯 What You'll Practice

- Understanding how strings are stored in memory as character arrays
- Declaring and initializing strings in different ways
- Reading strings with `scanf` and `fgets`
- Using common string functions: `strlen`, `strcpy`, `strcat`, `strcmp`, `strncmp`
- Writing your own versions of `strlen` and `strcat` from scratch
- Reversing a string, counting characters, and applying simple string-based rules

---

## 1. What Is a String in C?

Unlike many other languages, C does **not** have a built-in `string` type. A string in C is simply a **character array** that ends with the null terminator `'\0'`.

```c
#include <stdio.h>
int main() {
    char text[20];                  // Declaration (19 chars plus '\0' terminator)
    char text2[] = "Hello Ahmed!";  // Initialized — size auto-calculated

    return 0;
}
```

> 💡 When you write a string literal like `"Hello Ahmed!"` between double quotes, C automatically appends `'\0'` at the end for you. So `"Hello Ahmed!"` actually takes **13** characters in memory, not 12.

### How a String Looks in Memory

Take the string `"HELLO!"`. Here is exactly how it sits in a `char` array:

```
 Index:    0     1     2     3     4     5     6
        +-----+-----+-----+-----+-----+-----+------+
        | 'H' | 'E' | 'L' | 'L' | 'O' | '!' | '\0' |
        +-----+-----+-----+-----+-----+-----+------+
```

> ⚠️ **Without the `'\0'`**, C functions like `strlen` or `printf("%s", ...)` keep reading past the end of your array into garbage memory — until they accidentally find a zero byte somewhere. Always make sure your strings are properly terminated.

---

## 2. Reading and Manipulating Strings

C gives you a small set of helper functions in `<string.h>` for working with strings:

| Function | What It Does |
|----------|--------------|
| `strlen(s)` | Returns the length of `s` (not counting `'\0'`) |
| `strcpy(dest, src)` | Copies `src` into `dest` |
| `strcat(dest, src)` | Appends `src` to the end of `dest` |
| `strcmp(s1, s2)` | Compares two strings (returns `0` if equal) |
| `strncmp(s1, s2, n)` | Compares the first `n` characters |
### Reading a String from the User

There are several ways to read a string in C, but they differ in whether they handle spaces and whether they're safe from buffer overflows.

```c
#include <stdio.h>

int main() {
    char input[20];

    // scanf("%s", input);        // stops at the first space
    // scanf("%[^\n]", input);    // reads until '\n', but no size limit
    // gets(input);               // removed from the C standard — not recommended use
    fgets(input, 20, stdin);      // ✅ reads a full line, with a size limit

    printf("%s\n", input);
    return 0;
}
```

| Method | Reads spaces? | Safe? | Why |
|---|---|---|---|
| `scanf("%s", ...)` | ❌ | ⚠️ | No size limit — can overflow the array |
| `scanf("%[^\n]", ...)` | ✅ | ⚠️ | Reads until `'\n'`, but no size limit |
| `gets(name)` | ✅ | ❌ | No way to limit input size; removed from the standard |
| `fgets(name, 20, stdin)` | ✅ | ✅ | You pass the maximum size, so it can't overflow |

> 💡 With `scanf("%s", ...)`, you don't need `&` — the array name already decays to its address.
>
> ⚠️ `fgets` keeps the trailing newline. If the user types `ahmed mohamed` and presses Enter, the buffer holds `"ahmed mohamed\n\0"`. Strip the `'\n'` yourself if you don't want it.

### Quick Example — `strlen` in Action

```c
#include <stdio.h>
#include <string.h>

int main() {
    char text[] = "Hello Ahmed!";
    int len = strlen(text);
    printf("Length: %d\n", len);    // Length: 12
    return 0;
}
```

### Quick Example — `strcat` in Action

```c
#include <stdio.h>
#include <string.h>

int main() {
    char dest[50] = "Hello, ";
    char src[]    = "World!";
    strcat(dest, src);              // dest is now "Hello, World!"
    printf("%s\n", dest);
    return 0;
}
```

> ⚠️ The destination array (`dest`) **must be big enough** to hold both strings combined plus the `'\0'`. Otherwise you overflow and corrupt memory.

---

## 🧪 Exercises

---

### Exercise 1: Length of a String Without `strlen()`

**Task:** Write a C program that calculates the length of a string **without** using the built-in `strlen()` function.

<details markdown="1">
<summary>💡 Hint</summary>

- A string ends at `'\0'`. So just **walk through** the array, character by character, and count until you hit `'\0'`.
- Use a counter variable `i` that starts at `0` and increases each step.
- The condition for the loop is `s[i] != '\0'`.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main()
{
    char s[] = "okayy";
    int i = 0;
    while (s[i] != '\0')
    {
        i++;
    }
    printf("count: %d\n", i);
    return 0;
}
```

**How it works:**
- `i` starts at `0`.
- Each loop iteration checks the character at index `i`.
- As long as it isn't `'\0'`, we increment `i`.
- When the loop ends, `i` is exactly the number of characters before `'\0'` — i.e., the length.

**Output for `"okayy"`:**

```
count: 5
```

</details>

---

### Exercise 2: Concatenate Two Strings Without `strcat()`

**Task:** Write a C program that concatenates two strings **without** using the built-in `strcat()` function.

<details markdown="1">
<summary>💡 Hint</summary>

- Find the **end** of the first string (`str2`) using its length — that's where you'll start writing.
- Then copy each character of `str1` into `str2`, one by one, starting at that end position.
- Keep going until you've also copied the `'\0'` from `str1` — that's why the loop uses `<=` instead of `<`.
- ⚠️ Make sure `str2` is declared big enough to hold both strings combined plus the `'\0'`.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>
#include <string.h>

int main(){
    char str2[20] = "okay1|";
    char str1[]   = "okay2";
    int len1 = strlen(str1);
    int j    = strlen(str2);

    for (int i = 0; i <= len1; i++)   // <= to also copy the '\0' at the end
    {
        str2[j] = str1[i];
        j++;
    }
    printf("%s\n", str2);
    return 0;
}
```

**Why `i <= len1` and not `i < len1`?**
Because we also want to copy the `'\0'` of `str1` so that `str2` ends properly. If we stop at `< len1`, the new combined string would have no terminator and `printf("%s")` would print garbage after it.

**Output:**

```
okay1|okay2
```

</details>

---

### Exercise 3: Reverse a String

**Task:** Write a C program to reverse a given string.

<details markdown="1">
<summary>💡 Hint</summary>

There are two natural ways to do this:

1. **In-place swap:** swap the first character with the last, the second with the second-last, and so on. You only need to loop up to `length / 2`.
2. **Print in reverse without modifying:** loop from the last index down to `0` and just print each character. The original array stays unchanged.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>
#include <string.h>

// Solution 1 — actually reverses the array
void reverseString(char str[]) {
    int length = strlen(str);
    for (int i = 0; i < length / 2; i++) {
        // swap str[i] with str[length - i - 1]
        char temp = str[i];
        str[i] = str[length - i - 1];
        str[length - i - 1] = temp;
    }
}

// Solution 2 — only prints in reverse (does NOT modify the original)
void reverseString2(char str[]) {
    int length = strlen(str);
    for (int i = length - 1; i >= 0; i--) {
        printf("%c", str[i]);
    }
}

int main(){
    char str[] = "teacher";
    reverseString2(str);          // prints: rehcaet
    reverseString(str);           // now str itself becomes "rehcaet"
    printf("\n%s\n", str);
    return 0;
}
```

**Why only `length / 2`?**
Because each swap fixes **two** characters at once (one from the front, one from the back). If you looped all the way to `length`, you'd swap everything back to where it started!

**Trace for `"teacher"` (length 7):**

```
i = 0:  swap 't' and 'r'  →  "reachet"   (wait, let's do it properly)

Original:  t  e  a  c  h  e  r
Indices:   0  1  2  3  4  5  6

i = 0: swap [0] and [6]  → r e a c h e t
i = 1: swap [1] and [5]  → r e a c h e t  → r e a c h e t (e and e, no change)
i = 2: swap [2] and [4]  → r e h c a e t

Final:     r  e  h  c  a  e  t
```

</details>

---

### Exercise 4: Count Occurrences of a Character

**Task:** Write a C program to count how many times a specific character appears in a string.

<details markdown="1">
<summary>💡 Hint</summary>

- Loop through the string until you hit `'\0'`.
- Each iteration: check if the current character equals the **target** character. If yes, increment a counter.
- At the end, print the counter.

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>

int main()
{
    char str[]   = "ahmad";
    char target  = 'a';
    int count    = 0;

    for (int i = 0; str[i] != '\0'; i++)
    {
        if (str[i] == target)
        {
            count++;
        }
    }
    printf("Count: %d", count);
    return 0;
}
```

**Trace for `"ahmad"` looking for `'a'`:**

| `i` | `str[i]` | Match? | `count` |
|-----|----------|--------|---------|
| 0 | `'a'` | ✅ yes | `1` |
| 1 | `'h'` | ❌ no | `1` |
| 2 | `'m'` | ❌ no | `1` |
| 3 | `'a'` | ✅ yes | `2` |
| 4 | `'d'` | ❌ no | `2` |
| 5 | `'\0'` | loop stops | — |

**Output:**

```
Count: 2
```

</details>

---

### Exercise 5: Verb → Past Tense

**Task:** Write a program that takes verbs and forms their past tense based on these rules:

1. If a verb ends in `"e"` → add `"d"`.
2. If a verb ends in `"ss"` or `"gh"` → add `"ed"`.
3. In all other cases → tell the user the verb **may have an irregular past tense**.

Print each verb and its past tense. Test with this data:

```
smile  discuss  confess  declare  laugh  run  cough  teach  buy
```

<details markdown="1">
<summary>💡 Hint</summary>

- Use `strlen` to find the length of the verb.
- Look at the **last character** (`verb[length - 1]`) and the **second-to-last character** (`verb[length - 2]`) to decide which rule applies.
- Use `strcat(verb, "d")` or `strcat(verb, "ed")` to add the ending.
- ⚠️ Make sure the array has enough extra space for the added letters!

</details>

<details markdown="1">
<summary>🟢 Click to Show Solution</summary>

```c
#include <stdio.h>
#include <string.h>

void past(char verb[]) {
    int length = strlen(verb);

    if (verb[length - 1] == 'e') {
        strcat(verb, "d");
    } else if (length >= 2 && verb[length - 2] == 's' && verb[length - 1] == 's') {
        strcat(verb, "ed");
    } else if (length >= 2 && verb[length - 2] == 'g' && verb[length - 1] == 'h') {
        strcat(verb, "ed");
    } else {
        printf("The past tense of '%s' may have an irregular past tense\n", verb);
        return;
    }
    printf("The past tense is %s\n", verb);
}

int main(){
    char verbs[][20] = {"smile", "discuss", "confess", "declare",
                        "laugh", "run", "cough", "teach", "buy"};
    int verbsCount = 9;     // or use sizeof(verbs)/sizeof(verbs[0])

    for (int i = 0; i < verbsCount; i++) {
        past(verbs[i]);
    }
    return 0;
}
```

**Why check `length >= 2` before looking at `verb[length - 2]`?**
To avoid reading from a negative index when the verb has only 1 character.

**Expected output:**

```
The past tense is smiled
The past tense is discussed
The past tense is confessed
The past tense is declared
The past tense is laughed
The past tense of 'run' may have an irregular past tense
The past tense is coughed
The past tense of 'teach' may have an irregular past tense
The past tense of 'buy' may have an irregular past tense
```

**How each verb is decided:**

| Verb | Last char | 2nd last | Rule applied | Result |
|------|-----------|----------|--------------|--------|
| `smile` | `'e'` | — | rule 1 (+d) | `smiled` |
| `discuss` | `'s'` | `'s'` | rule 2 (+ed) | `discussed` |
| `confess` | `'s'` | `'s'` | rule 2 (+ed) | `confessed` |
| `declare` | `'e'` | — | rule 1 (+d) | `declared` |
| `laugh` | `'h'` | `'g'` | rule 2 (+ed) | `laughed` |
| `run` | `'n'` | `'u'` | none | irregular |
| `cough` | `'h'` | `'g'` | rule 2 (+ed) | `coughed` |
| `teach` | `'h'` | `'c'` | none | irregular |
| `buy` | `'y'` | `'u'` | none | irregular |

</details>

---

> ⬅️ [Back to Home](index.html)