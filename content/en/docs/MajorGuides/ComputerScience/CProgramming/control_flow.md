---
title: "Control Flow"
linkTitle: "Control Flow"
author: "Ben Grant"
date: 2021-09-16T23:07:22-07:00
weight: 1
icon:
draft: true
description: >
  If, switch, for, while
---

Control flow is how you can repeatedly or conditionally execute code in C.

## Statements and blocks

Most of C's control flow constructs accept either a statement or a block. A statement is a single line of C code, ending in a semicolon. A block is a group of statements surrounded by curly brackets. C variables are _block scoped_, which means that, if a variable is declared inside a block, it may only be used inside that block. Here's an example:

```c
void block_demonstration(void) {
    int a = 0;

    {
        a = 1; // okay
        int b = 2;

        {
            b = 3; // okay
            int c = 4;
        }

        c = 5; // error!
    }

    a = 6; // okay
    b = 7; // error!
    c = 8; // error!
}
```

## Conditions

Control flow statements require conditions which may evaluate to true or false. Any nonzero value is considered true. Originally, C did not have booleans, so zero was used for false and one for true. Since C99, you can use booleans by including `stdbool.h`:

```c
#include <stdbool.h>

int main(void) {
    bool one_bool = true;
    bool another_bool = false;
    bool yet_another_bool = (2 < 3); // true
    return 0;
}
```

The following operators are helpful in control flow statements:

| Precedence | Syntax       | Meaning                              |
|-----------:|--------------|--------------------------------------|
|          1 | `!condition` | `condition` is false                 |
|          2 | `a < b`      | `a` is less than `b`                 |
|          2 | `a <= b`     | `a` is less than or equal to `b`     |
|          2 | `a > b`      | `a` is greater than `b`              |
|          2 | `a >= b`     | `a` is greater than or equal to `b`  |
|          3 | `a == b`     | `a` and `b` are equal                |
|          3 | `a != b`     | `a` and `b` are not equal            |
|          4 | `a && b`     | `a` and `b` are both true            |
|          5 | `a \|\| b`   | `a` or `b` is true, or both are true |
<!-- backslashes on the previous line were required, otherwise the pipes are interpreted as cell boundaries -->

Operators with lower precedence are grouped first. For instance, since `&&` has lower precedence than `||`, the expression `a && b || c && d` is equivalent to `(a && b) || (c && d)`, not `a && (b || c) && d`. TODO explain associativity (operators with same precedence)?

Other things to note with these operators:

- An easy mistake is to use a single equals sign for equality, instead of two, like `if (a = b)`. That code will set `a` to `b`, and then use the new value of `a` as the condition, which is not invalid C (so it will compile), but it is probably not the behavior you want.
- The logical AND (`&&`) and OR (`||`) operators employ _short-circuiting_:
    - If the left operand in an AND is false, the right operand will not be evaluated, since there is no way it could make the whole statement true. For instance, in the condition `false && my_function()`, `my_function` will never be called.
    - If the left operand in an OR is true, the right operand will not be evaluated, since there is no way it could make the whole statement false. For instance, in the condition `true || my_function()`, `my_function` will never be called.
- The comparison operators don't work on strings, since strings are just pointers to character arrays and comparing the pointers does not tell you anything about how the actual contents of the strings compare. You can use [`strcmp`](https://linux.die.net/man/3/strcmp) to compare strings.

## If

The syntax for an if statement is `if (condition)`. The following code will be executed if `condition` evaluates to a non-zero value (NULL is zero).

```c
#include <stdio.h>
#include <stdbool.h>

int main(void) {
    // one statement
    if (false) printf("this is not printed\n");

    // block
    if (true) {
        printf("this is printed\n");
    }

    // comparisons
    if (2 < 3) {
        printf("this is printed\n");
    }

    return 0;
}
```

TODO else, else if

## While

A while loop runs as long as its condition is true. The standard while loop is known as a top-test loop_, as the condition is checked _before_ each iteration. So if the condition is false right away, the code inside the loop will never run. Here's how it looks:

```c
#include <stdio.h>

int main(void) {
    int i = 0;
    while (i <= 5) {
        printf("%d\n", i);
        i++;
    }

    return 0;
}
```

This program will print:

```
0
1
2
3
4
5
```

## Do-while

The do-while loop is similar to the while loop, except the condition is evaluated _after_ each iteration of the loop, making it a _bottom-test loop_. This means that the code inside the loop is guaranteed to run at least once, and then after each iteration, the condition is checked to see if it should run again.

```c
#include <stdio.h>

int main(void) {
    int i = 0;
    printf("running first loop\n");

    do {
        printf("first loop iteration\n");
    } while (i != 0);

    printf("running second loop\n");

    do {
        printf("%d\n", i);
        i++;
    } while (i <= 5);

    return 0;
}
```

Output:

```
running first loop
first loop iteration
running second loop
0
1
2
3
4
5
```

Do-while loops are much less commonly used than standard while loops, but they are sometimes useful.

## For loop

A for loop is a specialized while loop with additional functionality for the types of loops that are common. The syntax is `for (initialization; test; increment)`. It has three parts:

- **initialization:** code run before the first iteration.
- **test:** the condition to keep the loop running. Like while loops, for loops are top-test loops, so this condition is checked before each iteration.
- **increment:** code run after each iteration.

All three parts are technically optional, although most for loops use all three. Most for loops also have a single variable which all three parts use. Perhaps the most common for loop simply runs the code inside a given number of times:

```c
for (int i = 0; i < 5; i++) {
    // loop body
}
```

This loop will iterate 5 times, and `i` will take on the values from `0` to `4`, inclusive.

## Switch-case statement

The switch-case statement lets you execute one block of code depending on the value of a variable. Note that this works the same way as the normal equality operator (`==`), so it will not work for strings.

A `switch` statement contains `case` statements for different values that the variable could be. If one of the `case` statements matches, the code after that statement is run until the next `break` statement (more on `break` in the next section). If no value matches, it jumps to the `default` statement, if there is one.

```c
#include <stdio.h>

int main(void) {
    int i = 4;
    switch (i) {
    case 1:
        printf("i is 1\n");
        break;
    case 2:
    case 3:
        printf("i is 2 or 3\n");
        break;
    case 4:
        printf("i is 4\n");
        break;
    case 5:
        printf("i is 5\n");
        // no break, so we keep going even after the next case
    case 6:
        printf("i is 5 or 6\n");
        break;
    default:
        printf("i is something else\n");
    }

    return 0;
}
```

## Additional resources

More on operators - https://en.cppreference.com/w/c/language/operator_precedence
