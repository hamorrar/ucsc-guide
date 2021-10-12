---
title: "C Programming"
linkTitle: "C Programming"
author: "Brian Mak, Ben Grant"
date: "2021-09-10"
weight: 1
icon:
draft: false
description: >
  Introduction to C programming.
---

This section is designed as an introduction into C for use in lower division courses, such as CSE 13S. This section will link to official reference and other resources when possible.

---

## Prerequisites

- A basic understanding of programming concepts, such as variables, if statements, loops, and functions. If you do not have *any* programming experience, it is *highly* recommended that you read the section on Python first.
- A Linux virtual machine or box. (Ubuntu 20.04 recommended)
- A basic understanding of how the terminal works on your distribution of Linux. If you do have not used a Linux before, it is recommended that you read the section on Unix first.

---

## Background

[C](https://en.wikipedia.org/wiki/C_\(programming_language\)) is a a very simple language. It was developed in the 1970s by [Dennis Ritchie](https://en.wikipedia.org/wiki/Dennis_Ritchie). The language was eventually standardized in 1989 by [ANSI](https://en.wikipedia.org/wiki/American_National_Standards_Institute). This version would become known as ANSI C, also referred to as C89. Over the years, newer versions of the C standard have been published. This section will primarily be covering basic C features up until C99.

---

## Hello world

```c {linenos=table}
#include <stdio.h>

int main(void) {
    printf( "Hello World!\n" );

    return 0;
}
```

The above code shows one of the ways to write a "Hello World" program in C. A "Hello World" program is a program that prints "Hello World" or some variation to the terminal. This program may look a little intimidating at first for someone who hasn't seen C code before, but rest assured, each part of the code will be explained eventually through this section's articles.

Line 1 shows a ``#include`` preprocessor directive. The ``#include`` directive will be covered more in-depth in the "Writing programs" section. Preprocessor directives in general will be covered later in the "Building programs" section. For now, all you need to know about this line is that it enables us to use the ``printf`` function.

Line 3 shows a function signature. A function signature contains information about a function. This function in specific is called the main function. When defined, it is the function that is called when the program is run. Functions will be covered later in the "Functions" section.

Line 4 shows a call to the ``printf`` function. In this case, ``printf`` is used to print (output) ``"Hello World!\n"`` to the standard output. Standard output will be explained in the "Standard Input/Output/Error" section. ``\n`` is put at the end to print a new line. Unlike many other programming languages' print statements/functions/methods, C's ``printf`` does not automatically add a new line at the end of the string to be printed. You will need to do so manually.

Line 6 makes the program return with error code 0. In C, the main function returns error codes. An error code of 0 indicates that the program exited *without* an error. A non-zero error code indicates that the program exited *with* an error. Return statements and values will be covered more in-depth in the "Functions" section.

If you are still confused about how this program works, do not worry. Each part of it will eventually be covered in this section's articles.

## Additional resources

The definitive book on C is _The C Programming Language_, by Brian Kernighan and Dennis Ritchie (the book is often called "K&R" after the author's last initials). It's concise, well-written, and generally a model for excellent technical writing. The second and most recent edition was published all the way back in 1988, but C has not changed much since then, so it is still a great resource. It can easily be found legally (for money) or illegally (for free) online.
