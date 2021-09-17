---
title: "Control Flow"
linkTitle: "Control Flow"
author: "Ben Grant"
date: 2021-09-16T23:07:22-07:00
weight: 1
icon:
draft: false
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

void if_statements(void) {
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
}
```

## While

A while loop runs as long as its condition is true. The standard while loop is known as a _pre-test loop_, as the condition is checked _before_ each iteration. So if the condition is false right away, the code inside the loop will never run.

TODO examples

## Do while

The do while loop is similar to the while loop, except the condition is evaluated _after_ each iteration of the loop. This means that the code inside the loop is guaranteed to run at least once, and then after each iteration, the condition is checked to see if it should run again.

TODO examples

## For loop

A for loop is a specialized while loop with additional functionality. It has three parts:

TODO finish this lol

## Additional resources

More on operators - https://en.cppreference.com/w/c/language/operator_precedence
