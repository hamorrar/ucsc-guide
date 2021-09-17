---
title: "Functions"
linkTitle: "Functions"
author: "Ben Grant"
date: 2021-09-16T01:06:15-07:00
weight: 1
icon:
draft: false
description: >
  C functions, static variables, and function pointers
---

Functions in C are similar to functions in other languages. They can accept arguments, and optionally return a single value. Of course, the types of all arguments and the return value must be specified.

## Syntax

C's function syntax will be familiar to Java or C# programmers. Here's one of the simplest functions:

```c
void print_hello(void) {
    printf("Hello\n");
}
```

The first `void` is the return value, meaning that the function returns nothing. The second `void` is where the argument list goes. An empty argument list in C (like `void print_hello()`) actually means that the function can accept any number of arguments, so you should specify `void` for a function that takes no arguments.

Here is a function that takes arguments and returns a value:

```c
int add_squares(int a, int b) {
    return (a * a) + (b * b);
}
```

## Declarations vs. definitions

The examples above were function _definitions_, because they both defined the code inside the functions (the function bodies). Sometimes you will want to _declare_ that a function exists before actually defining it. [TODO link to section on source/header files] A function declaration is written just like a definition, except you put a semicolon after the closing parenthesis instead of the curly braces and function body. Here are declarations for the two functions above:

```c
void print_hello(void);
int add_squares(int a, int b);
```

If a function has been declared but not defined, you can still compile code that calls the function, because the compiler knows how the function should be called and can check that you're calling it correctly. But the linker will fail if you don't have a definition for the function.

## The `main` function

`main` is a special function in C. It's the "entry point," meaning that the operating system will call your `main` function when it runs your program. As such, any C program must contain a `main` function.

[As shown in the Hello World example]({{< ref "./_index.md#hello-world" >}}), the return type of `main` is `int`, and it should return zero if the program ran correctly. Conventionally, if a fatal error occurs, you return early from `main` with a non-zero value (you might designate different numbers to indicate different types of errors). `main` also optionally takes two arguments, which let your program access arguments passed to it on the command line:

```c
int main(int argc, char *argv[]) {
    printf("%s\n", argv[0]);
    return 0;
}
```

`argc` is the number of arguments that were passed, and `argv` is a string array containing them all. The first argument is actually the name that was used to invoke your program, which means that the first "actual" argument will have index 1. Here are some example program invocations followed by the arguments that get passed to `main` in each case:

```
$ ./foo
argc = 1
argv = ["./foo"]

$ ls -l Documents/
argc = 3
argv = ["ls", "-l", "Documents/"]

$ ./myprogram hello world
argc = 3
argv = ["./myprogram", "hello", "world"]

$ ./myprogram 'hello world'
argc = 2
argv = ["./myprogram", "hello world"]
```

## Static variables

Usually, when you call a function, a new _stack frame_ is created with space for all the variables that function uses (including arguments), and pushed onto the _call stack_. This means that each invocation of a function has its own copy of the different variables. Consider the following program:

```c
#include <stdio.h>

int count(void) {
    int counter = 0;
    counter++;
    return counter;
}

int main(void) {
    printf("%d\n", count());
    printf("%d\n", count());
    printf("%d\n", count());
    return 0;
}
```

Each call to `count` has its own version of `counter`, so although they all increment `counter`, the incremented version is lost as soon as the function returns, and the next invocation starts again with `counter` set to zero. Here is what this outputs:

```
1
1
1
```

Now let's make `counter` a static variable:

```c
#include <stdio.h>

int count(void) {
    static int counter = 0;
    counter++;
    return counter;
}

int main(void) {
    printf("%d\n", count());
    printf("%d\n", count());
    printf("%d\n", count());
    return 0;
}
```

When a variable is declared `static`, there will only be one copy of the variable. It's a lot like a global variable, except it can only be accessed inside the function. Running this version of the program, we can see that the value of `counter` is kept from one call to the next:

```
1
2
3
```

## Function pointers

TODO
