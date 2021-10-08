---
title: "Compilation"
linkTitle: "Compilation"
author: "Ben Grant"
date: 2021-10-08T12:06:29-07:00
weight: 1
icon:
draft: true
description: >
  Compilation, linking, header files, object files, and Makefiles
---

This page describes how to compile C programs that are more complex than a single source file. We'll cover how to split code across multiple files, how to compile those files, how to automate the build process using GNU make, and how to make use of system libraries.

You can follow along with this guide on your own computer. All you'll need is familiarity with the command line and a C programming environment with recent versions of clang and make. I would recommend using Linux (either running on your computer, in a virtual machine, or in WSL2). These commands may also work on macOS if you install clang and make, but they will _not_ work on Windows if you don't have a Linux environment.

## Our program

To get started, create an empty directory to hold all the files that we create. The name doesn't matter. Navigate into that directory, and create the following C file called `hypot.c`. This is the program that we will be working with. Given two side lengths of a right triangle, it calculates the length of the hypotenuse.

```c
// hypot.c
#include <stdio.h>
#include <stdlib.h>

// approximation of sqrt(x) for some values of x
unsigned int sqrts[] = {
    0,
    1, 1,
    2, 2, 2, 2,
    3, 3, 3, 3, 3, 3,
    4, 4, 4, 4, 4, 4, 4, 4,
    5, 5, 5, 5, 5,
};

unsigned int my_sqrt(unsigned int x) {
    if (x > 25) {
        fprintf(stderr, "error: cannot take sqrt of %u\n", x);
        exit(2);
    }
    return sqrts[x];
}

double my_hypot(double a, double b) {
    return my_sqrt(a * a + b * b);
}

int main(void) {
    double a, b;
    printf("side a: ");
    if (!scanf("%lf", &a)) {
        fprintf(stderr, "invalid input\n");
        return 1;
    }
    printf("side b: ");
    if (!scanf("%lf", &b)) {
        fprintf(stderr, "invalid input\n");
        return 1;
    }

    printf("c = %lf\n", my_hypot(a, b));
    return 0;
}
```

You may already know the command to compile this using clang:

```bash
$ clang -Wall -Werror -Wextra -Wpedantic -o hypot hypot.c
```

But what does every part of this mean? clang, like most command line programs, lets you specify _input files_ (in this case, C files to compile) as well as _flags_ that modify its behavior. Each argument that isn't part of a flag is interpreted as an input file. Let's break down all the arguments:

- `-Wall`, `-Werror`, `-Wextra`, `-Wpedantic`: each of these enables a certain class of warnings. Together, they make clang very strict. With these flags, compilation will often fail when issues are encountered that would normally only be treated as warnings.
- `-o`,  `hypot`: the `o` stands for "output," and means that the next argument should be used as the output filename. This makes clang save the executable file as `hypot`, and prevents `hypot` from being interpreted as an input filename.
- `hypot.c`: this is the only input file.

The compilation should succeed without errors. Now you can run the program:

```
$ ./hypot
side a: 3
side b: 4
c = 5.000000
```

It worked! But, as you might have noticed from the code, our calculation is extremely limited—the square root function only returns integer approximations for numbers between 0 and 25, and fails on any other numbers. We're going to modify this program to:

- use the built-in math library's `sqrt` function
- move the `my_hypot` function into another file
- automatically compile with all the right parameters when we run `make`

## Using the math library

You may know that in order to call math functions like `sqrt`, you need to do two things: put `#include <math.h>` at the top of your file, and add `-lm` to your compilation flags. What do these do?

### Header files

Including a file with `#include` inserts its contents at the position of the `#include` statement, nothing more. Since `<math.h>` uses angle brackets instead of quotes, the preprocessor (which is responsible for processing includes, among other things) looks for a file in the _include path_, instead of the current directory. You can modify the include path, but the default (on Linux, at least) is `/usr/include`. This means that we are including `/usr/include/math.h`, a file that is included with the operating system. You can actually open and view this file! Sadly, it is full of macros and includes other files, so the actual declaration of `sqrt` is not easy to find, but you can imagine that somewhere in that file is the declaration:

```c
double sqrt(double x);
```

(Since the preprocessor processes includes recursively, as far as you are concerned, that declaration may as well actually be in `/usr/include/math.h`. The fact that it isn't is transparent to you.)

Let's change our program to use the system's `sqrt` function (to make this tutorial easier to follow, when you modify a file, I'll specify what the complete contents should now be):

```c
// hypot.c
#include <stdio.h>
#include <stdlib.h>
// new line
#include <math.h>

// deleted: sqrts array and my_sqrt function

double my_hypot(double a, double b) {
    // modified
    return sqrt(a * a + b * b);
}

int main(void) {
    double a, b;
    printf("side a: ");
    if (!scanf("%lf", &a)) {
        fprintf(stderr, "invalid input\n");
        return 1;
    }
    printf("side b: ");
    if (!scanf("%lf", &b)) {
        fprintf(stderr, "invalid input\n");
        return 1;
    }

    printf("c = %lf\n", my_hypot(a, b));
    return 0;
}
```

### Linking against a system library

Let's recompile:

```
$ clang -Wall -Wextra -Werror -Wpedantic hypot.c -o hypot
/usr/bin/ld: /tmp/hypot-1e886c.o: in function `my_hypot':
hypot.c:(.text+0x2b): undefined reference to `sqrt'
clang-12: error: linker command failed with exit code 1 (use -v to see invocation)
```

Uh oh! The important part of this error is <code>undefined reference to \`sqrt'</code>. Remember that `math.h` contains only the declaration of `sqrt`. That essentially tells the compiler that there _will be_ a function available, called `sqrt`, returning a `double`, and taking one `double` as its argument. However, to finish linking the binary, the linker needs to know what the address of that function will be at runtime, so that it can insert the proper function call. (We'll get into the difference between compiling and linking later. For now, know that `clang -Wall -Wextra -Werror -Wpedantic hypot.c -o hypot` runs both steps, compiling and then linking your C file).
