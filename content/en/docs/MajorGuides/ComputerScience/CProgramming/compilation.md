---
title: "Compilation"
linkTitle: "Compilation"
author: "Ben Grant"
date: 2021-10-12T00:00:00-07:00
weight: 1
icon:
draft: false
description: >
  Compilation, linking, header files, object files, and Makefiles
---

This page describes how to compile C programs that are more complex than a single source file. We'll cover how to split code across multiple files, how to compile those files, how to automate the build process using GNU Make, and how to make use of system libraries.

You can follow along with this guide on your own computer. All you'll need is familiarity with the command line and a C programming environment with recent versions of Clang and Make. I would recommend using Linux (either running on your computer, in a virtual machine, or in WSL2). These commands may also work on macOS if you install Clang and Make, but they will _not_ work on Windows if you don't have a Linux environment.

## Our program

To get started, create an empty directory to hold all the files that we create. The name doesn't matter. Navigate into that directory and create the following C file called `hypot.c`. This is the program that we will be working with. Given two side lengths of a right triangle, it calculates the length of the hypotenuse.

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

You may already know the command to compile this using Clang:

```
$ clang -Wall -Werror -Wextra -Wpedantic -o hypot hypot.c
```

But what does every part of this mean? Clang, like most command line programs, lets you specify _input files_ (in this case, C files to compile) as well as _flags_ that modify its behavior. Each argument that isn't part of a flag is interpreted as an input file. Let's break down all the arguments:

- `-Wall`, `-Werror`, `-Wextra`, `-Wpedantic`: each of these enables a certain class of warnings. Together, they make Clang very strict. With these flags, compilation will often fail when issues are encountered that would normally only be treated as warnings.
- `-o`,  `hypot`: the `o` stands for "output," and means that the next argument should be used as the output filename. This makes Clang save the executable file as `hypot`, and prevents `hypot` from being interpreted as an input filename.
- `hypot.c`: this is the only input file.

The compilation should succeed without errors. Now you can run the program:

```
$ ./hypot
side a: 3
side b: 4
c = 5.000000
```

It worked! But, as you might have noticed from the code, our calculation is extremely limited—the square root function only returns integer approximations for numbers between 0 and 25, and fails on any other numbers. Here's an example:

```
$ ./hypot
side a: 2
side b: 2
c = 3.000000
```

The side length should be &radic;8 &approx; 2.828. We're going to modify this program to:

- use the built-in math library's `sqrt` function
- move the `my_hypot` function into another file
- automatically compile with all the right parameters when we run `make`

## Using the math library

You may know that in order to call math functions like `sqrt`, you need to do two things: put `#include <math.h>` at the top of your file, and add `-lm` to your compilation flags. What do these do?

### Header files

Including a file with `#include` inserts its contents at the position of the `#include` statement, nothing more. Since `<math.h>` uses angle brackets instead of quotes, the preprocessor (which is responsible for processing includes, among other things) looks for a file in the _include path_, instead of the current directory. You can modify the include path, but the default (on Linux, at least) is `/usr/include`. This means that we are including `/usr/include/math.h`, a file that comes with the operating system. You can actually open and view this file! Sadly, it is full of macros and includes other files, so the actual declaration of `sqrt` is not easy to find, but you can imagine that somewhere in that file is the declaration:

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

We can fix this error by _linking against_ the math library. This is a _shared library_, meaning that its code can be used by any program on your computer, and the code is loaded dynamically when the program runs instead of being part of the executable. (All modern operating systems have shared libraries, but they use different file extensions. On Linux they are `.so` files, macOS uses `.dylib`, and Windows uses `.dll`.) Each executable contains a list of shared libraries that should be loaded, and linking against a shared library just adds its name to this list.

Library names are prefixed with `lib`. The math library is `libm`. To link against a library, you use `-l` followed by the name of the library without the prefix, so the math library is `-lm`. Let's recompile with this flag:

```
$ clang -Wall -Wextra -Werror -Wpedantic hypot.c -o hypot -lm
```

This time, the program handles the entire range of square roots:

```
$ ./hypot
side a: 2
side b: 2
c = 2.828427
```

Besides the fact that compilation succeeded, how do we know that the math library was linked properly? There's a utility called `ldd` that lists which libraries a given executable links against. Let's try it on our `hypot` binary:

```
$ ldd hypot
        linux-vdso.so.1 (0x00007ffdc0912000)
        libm.so.6 => /usr/lib/libm.so.6 (0x00007fa15dbbd000)
        libc.so.6 => /usr/lib/libc.so.6 (0x00007fa15d9f1000)
        /lib64/ld-linux-x86-64.so.2 => /usr/lib64/ld-linux-x86-64.so.2 (0x00007fa15dd43000)
```

The exact output may differ from system to system, but you should at least see `libm` and `libc`. `libc` is the standard C library, and it is linked by default. That's why we can call functions like `printf` and `scanf` without any linker flags—they are part of `libc`.

Another interesting thing about this output is that it shows where each library is stored. On my system, they are all in `/usr/lib`. I tried this on an Ubuntu system and they were in `/lib/x86_64-linux-gnu` (suggesting that you could also have dynamic libraries installed for different CPU architectures). Fortunately, the system determines the exact path when your executable is running. This means I could copy my `hypot` executable onto an Ubuntu system (or copy an executable compiled on Ubuntu onto my system), and it would still find all the libraries it needs.

## Splitting up our program

We have successfully modified our program to use the system's `sqrt` function instead of our own janky one! All that remains is to, as promised, move the `my_hypot` function into its own file.

We'll create two new files: a header, `mathlib.h`, and a C file, `mathlib.c`. Insert the following contents:

```c
// mathlib.h
#pragma once

double my_hypot(double a, double b);
```

```c
// mathlib.c
#include "mathlib.h"

#include <math.h>

double my_hypot(double a, double b) {
    return sqrt(a * a + b * b);
}
```

The line `#pragma once` in `mathlib.h` ensures that the header file is only included once. It won't make a difference in this tutorial, but in more advanced programs where one header file includes another header file (e.g. to get type definitions), you may get errors about multiple definitions of the contents of a header without `#pragma once`.

We also need to include the header file (not the C file!) from our main `hypot.c`. Add the `#include` statement:

```c
// hypot.c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
// new line
#include "mathlib.h"

double my_hypot(double a, double b) {
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

We `#include` headers, not C files, because the C file is going to be compiled separately and linked. The file with the include statement only needs the declarations of functions, not definitions.

You may already be thinking of some other changes we'll have to make to `hypot.c`. Let's add `mathlib.c` as an input file to our last compilation command, and try compiling this:

```
$ clang -Wall -Wextra -Werror -Wpedantic hypot.c mathlib.c -o hypot -lm
/usr/bin/ld: /tmp/mathlib-5b7ded.o: in function `my_hypot':
mathlib.c:(.text+0x0): multiple definition of `my_hypot'; /tmp/hypot-96432d.o:hypot.c:(.text+0x0): first defined here
clang-12: error: linker command failed with exit code 1 (use -v to see invocation)
```

Zeroing in on that error, the main issue is <code>multiple definition of \`my_hypot'</code>. It says that one definition is in `mathlib.c` and another is in `hypot.c`. Let's remove the one in `hypot.c` (we also remove `#include <math.h>` since this file no longer needs to call `sqrt`):

```c
#include <stdio.h>
#include <stdlib.h>

#include "mathlib.h"

// my_hypot function removed

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

If we compile this using the same command as before, it works!

## Automating compilation with Make

We're almost ready to reduce our entire compilation process to just one command, but first we must learn one more concept.

### Object files

An executable file (like the `hypot` file that we are creating) contains several things:

- machine code for every function in your program
- an entry point (in C, the `main` function) where execution should begin
- data that the program will need when it runs (e.g. the `"side a: "`) string that we print
- space for global variables
- a list of dynamic libraries that should be loaded

An _object file_ is similar to an executable, but different in some important ways. At the fundamental level, object files still contain executable code. An executable file is your whole program, but for programs with multiple source files, an object file is the compiled version of a single C file. Since object files cannot run on their own, they don't have an entry point (they could have a function called `main`, however). Also, in an executable file, every function that's referenced must be defined either in the executable itself, or in a dynamic library that is linked. Object files can reference external functions.

To compile a C program, you _compile_ each C file into an object file, and then _link_ those object files into one executable. Even if you don't list these steps explicitly, Clang still performs both steps; it just deletes the object files when it's done. The linking process entails:

- combining all the code in the various object files, making sure there are no functions with the same name
- for each function call, figuring out where that function will actually be located (in the binary or in a dynamic library) at runtime
- making sure there is a `main` function, and marking it as the entry point
- producing the final binary

### Manually compiling and linking

First, let's run the commands to compile our C files to object files and link them. This is what make will eventually do for us.

The `-c` flag tells Clang to output an object file instead of an executable. By default, it will just replace `.c` with `.o`, but you can also specify the location of the object file manually with `-o`. Delete the `hypot` binary if you still have it from a previous section, and then let's compile `hypot.c` and see what it creates:

```
$ clang -Wall -Wextra -Werror -Wpedantic -c hypot.c
$ ls
hypot.c  hypot.o  mathlib.c  mathlib.h
```

Even though `hypot.c` uses functions from `mathlib.c`, it compiles just fine. But let's try linking it. The command to link object files is the same as the command to link C files, except you specify object files as input. We also omit the warning flags, since those only affect the compiler, not the linker.

```
$ clang hypot.o -o hypot
/usr/bin/ld: hypot.o: in function `main':
hypot.c:(.text+0xc1): undefined reference to `my_hypot'
clang-12: error: linker command failed with exit code 1 (use -v to see invocation)
```

It's complaining that it can't find the `my_hypot` function, since that is in a different file. Note that we got this error during linking and not compilation, since object files are allowed to reference functions from other files. Let's compile `mathlib.c` into an object file and try again:

```
$ clang -Wall -Wextra -Werror -Wpedantic -c mathlib.c
$ ls
hypot.c  hypot.o  mathlib.c  mathlib.h  mathlib.o
$ clang hypot.o mathlib.o -o hypot
/usr/bin/ld: mathlib.o: in function `my_hypot':
mathlib.c:(.text+0x2b): undefined reference to `sqrt'
clang-12: error: linker command failed with exit code 1 (use -v to see invocation)
```

Now it can find `my_hypot`, but it still can't find `sqrt` since we aren't linking the math library. We can add the `-lm` flag the same way as before:

```
$ clang -lm hypot.o mathlib.o -o hypot
$ ls
hypot  hypot.c  hypot.o  mathlib.c  mathlib.h  mathlib.o
```

It worked!

Currently, after changing our code, we would have to:

- recompile any C file(s) that we changed into new object files
- link all our object files (including ones that didn't change) into a new binary

This will become impractical quickly. [Let's automate it!](https://xkcd.com/1319/)

### Make

Make is a utility to automate your build process. It reads a Makefile (which is just a text file exactly called `Makefile`) for instructions on how to produce various files, and builds the one that you specified.

The true power of Make lies in its dependency system. You can specify the files that a file depends on (for instance, our binary `hypot` depends on the object files `hypot.o` and `mathlib.o`). When you use Make to build one file, it will automatically build all the file's dependencies. But it will also look at when the various files were modified, and avoid rebuilding dependencies that have not changed since the file that depends on them was rebuilt. In our example, this means that if we run `make`, change `hypot.c`, and run `make` again, it won't bother recompiling `mathlib.c`. This saves a lot of time for large programs!

We're going to build up our Makefile a little bit at a time. Create a file called `Makefile` with the following contents:

```makefile
CC = clang
CFLAGS = -Wall -Wextra -Werror -Wpedantic
LDFLAGS = -lm
EXEC = hypot
OBJS = hypot.o mathlib.o
```

These are variables that we'll use later in the Makefile.

- `CC` is the name of the C compiler that we use
- `CFLAGS` are the flags that are passed to the compiler
- `LDFLAGS` are the flags that are passed to the linker
- `EXEC` is the name of the executable file we are making
- `OBJS` is the list of object files that we want to compile and link

Let's add the next parts to our Makefile:

```makefile
CC = clang
CFLAGS = -Wall -Wextra -Werror -Wpedantic
LDFLAGS = -lm
EXEC = hypot
OBJS = hypot.o mathlib.o

$(EXEC): $(OBJS)
	$(CC) $(LDFLAGS) -o $(EXEC) $(OBJS)
```

Make sure the last line is indented with tabs, not spaces. Make requires tabs.

This looks complicated! The main thing going on is that `$(VAR)` gets replaced with the variable `VAR`. If we perform those replacements manually, those last two lines look like:

```makefile
hypot: hypot.o mathlib.o
	clang -lm -o hypot hypot.o mathlib.o
```

This is one _target_. A target begins with the line `target: dependencies`, so in this case we are saying that `hypot` is a target which depends on `hypot.o` and `mathlib.o`. After this line come the command(s) to build that file, indented with tabs. You can see that, after all the variables have been substituted, the command here is the same as we were already using to link the executable.

Let's keep going! Next we'll add targets to build our object files:

```makefile
CC = clang
CFLAGS = -Wall -Wextra -Werror -Wpedantic
LDFLAGS = -lm
EXEC = hypot
OBJS = hypot.o mathlib.o

$(EXEC): $(OBJS)
	$(CC) $(LDFLAGS) -o $(EXEC) $(OBJS)

hypot.o: hypot.c
	$(CC) $(CFLAGS) -c hypot.c

mathlib.o: mathlib.c
	$(CC) $(CFLAGS) -c mathlib.c
```

We list the C files as dependencies of these targets to ensure that each object file gets rebuilt when its corresponding C file changes. But unlike the previous example, the C files will not get their own targets in the Makefile, since those files are created by us and not Make. Since Make knows it isn't responsible for creating the C files, it will just check that each one exists before it tries to build the object file, and throw an error if one is missing.

We're going to add some more to the Makefile, but this is already enough to build our program! Let's try it out. To build a Make target, just run `make <target name>` in the directory containing the Makefile. If you don't specify a target, it will use the first one that is defined. In our Makefile, that is the `$(EXEC)` rule, so we are good to go. Make sure to delete your object files and executable, if you still have them from previous sections.

```
$ ls
hypot  hypot.c  hypot.o  Makefile  mathlib.c  mathlib.h  mathlib.o
$ rm hypot *.o
$ ls
hypot.c  Makefile  mathlib.c  mathlib.h
$ make
clang -Wall -Wextra -Werror -Wpedantic -c hypot.c
clang -Wall -Wextra -Werror -Wpedantic -c mathlib.c
clang -lm -o hypot hypot.o mathlib.o
$ ls
hypot  hypot.c  hypot.o  Makefile  mathlib.c  mathlib.h  mathlib.o
$ ./hypot
side a: 2
side b: 3
c = 3.605551
```

It worked! Note how Make prints out the commands that it runs. Let's try compiling it again:

```
$ make
make: 'hypot' is up to date.
```

It didn't recompile because it has already built everything that it needs, and we didn't change our C files.

### A more advanced Makefile

This Makefile works fine, but it can do more. We're going to make a few changes.

#### Separate `all` target

In a more advanced project, you might have multiple executable files that should be compiled. Right now, we couldn't run `make` to compile multiple executables, because it only runs the first target by default.

We can use something called a _phony target_ to remedy this. A phony target is a target that doesn't correspond to a single file. In this case, we create a target called `all` with all our executables (there is still only one, but there could be more) as dependencies, and put it first in the Makefile:

```makefile
CC = clang
CFLAGS = -Wall -Wextra -Werror -Wpedantic
LDFLAGS = -lm
EXEC = hypot
OBJS = hypot.o mathlib.o

all: $(EXEC)

$(EXEC): $(OBJS)
	$(CC) $(LDFLAGS) -o $(EXEC) $(OBJS)

hypot.o: hypot.c
	$(CC) $(CFLAGS) -c hypot.c

mathlib.o: mathlib.c
	$(CC) $(CFLAGS) -c mathlib.c
```

We've listed `hypot` as the sole dependency of the `all` target. If there were a file called `all` in our project, we would need to name this target something else, because Make would think that it had already been built. Note that there are no commands to build `all`, because it will still run the commands to build `hypot`. Feel free to try deleting the executable and/or object files and running `make` again.

#### Cleanup

It's common to include a target called `clean` that deletes all executables and object files. We'll do this using `rm` with the `-f` flag ("force"). The flag means that if we ask it to delete a file that doesn't exist, it will silently ignore that argument instead of producing an error, so we can still run our `clean` target even if there isn't anything for it to delete.

```makefile
CC = clang
CFLAGS = -Wall -Wextra -Werror -Wpedantic
LDFLAGS = -lm
EXEC = hypot
OBJS = hypot.o mathlib.o

all: $(EXEC)

$(EXEC): $(OBJS)
	$(CC) $(LDFLAGS) -o $(EXEC) $(OBJS)

hypot.o: hypot.c
	$(CC) $(CFLAGS) -c hypot.c

mathlib.o: mathlib.c
	$(CC) $(CFLAGS) -c mathlib.c

clean:
	rm -f $(EXEC) $(OBJS)
```

`clean` has no dependencies, and the command uses our variables to delete the files that it should. Let's try it, first using `make` to make sure our program is compiled.

```
$ make
make: Nothing to be done for 'all'.
$ ls
hypot  hypot.c  hypot.o  Makefile  mathlib.c  mathlib.h  mathlib.o
$ make clean
rm -f hypot hypot.o mathlib.o
$ ls
hypot.c  Makefile  mathlib.c  mathlib.h
```

#### Automatically compiling object files

Right now, if we added another C file to our program, we'd have to add a new target to our Makefile and copy the command to compile it. This can get unwieldy, and we run the risk of introducing a subtle bug by copying the command incorrectly.

Fortunately, Make allows us to specify much more general rules. Specifically, we can tell it how to compile any object file from the corresponding C file:

```makefile
CC = clang
CFLAGS = -Wall -Wextra -Werror -Wpedantic
LDFLAGS = -lm
EXEC = hypot
OBJS = hypot.o mathlib.o

all: $(EXEC)

$(EXEC): $(OBJS)
	$(CC) $(LDFLAGS) -o $(EXEC) $(OBJS)

%.o: %.c
	$(CC) $(CFLAGS) -c $<

clean:
	rm -f $(EXEC) $(OBJS)
```

The syntax here is tricky. The `%` symbols create a correspondence between the names of the object file and C file: any filename ending with `.o` depends on the same filename but with `.c` instead of `.o`. In the compilation command, `$<` gets replaced with the name of the dependency, i.e. the name of the C file.

Let's check that this works, using `make clean` first to make sure it has to recompile everything:

```
$ make clean
rm -f hypot hypot.o mathlib.o
$ ls
hypot.c  Makefile  mathlib.c  mathlib.h
$ make
clang -Wall -Wextra -Werror -Wpedantic -c hypot.c
clang -Wall -Wextra -Werror -Wpedantic -c mathlib.c
clang -lm -o hypot hypot.o mathlib.o
$ ls
hypot  hypot.c  hypot.o  Makefile  mathlib.c  mathlib.h  mathlib.o
```

And it does!

#### Formatting with clang-format

If you use [clang-format](https://clang.llvm.org/docs/ClangFormat.html) and have a configuration file (`.clang-format`) next to your code, you can add a target to run it with `make format` (here, the rest of the Makefile is omitted, since the target is not specific to our code):

```makefile
format:
	clang-format -i -style=file *.[ch]
```

#### Static analysis with scan-build

[scan-build](https://clang-analyzer.llvm.org/scan-build.html) is a program that detects additional problems with your code at compile time (that a compiler normally would not). We can also call it with a Makefile target:

```makefile
scan-build: clean
	scan-build --use-cc=$(CC) make
```

This target isn't as straightforward as the clang-format one. Some details to note are:

- scan-build's argument is the command that builds our program. Here, that is just `make`.
- We list `clean` as a dependency. This ensures that all object files and executables are deleted before we run scan-build, so when scan-build runs `make`, the whole program is rebuilt.
- scan-build sometimes overrides the compiler used by Make. We specify `--use-cc=$(CC)` (effectively `--use-cc=clang`) to make sure that it will run using the same compiler that we normally use (as opposed to, say, GCC).

Here's an example of running it:

```
$ make scan-build
rm -f hypot hypot.o mathlib.o
scan-build --use-cc=clang make
scan-build: Using '/usr/bin/clang-12' for static analysis
make[1]: warning: jobserver unavailable: using -j1.  Add '+' to parent make rule.
make[1]: Entering directory '/home/ben/code/c/ucsc-guide-hypot'
/usr/bin/../lib/clang/ccc-analyzer -Wall -Wextra -Werror -Wpedantic -c hypot.c
/usr/bin/../lib/clang/ccc-analyzer -Wall -Wextra -Werror -Wpedantic -c mathlib.c
/usr/bin/../lib/clang/ccc-analyzer -lm -o hypot hypot.o mathlib.o
make[1]: Leaving directory '/home/ben/code/c/ucsc-guide-hypot'
scan-build: Analysis run complete.
scan-build: Removing directory '/tmp/scan-build-2021-10-11-005941-146456-1' because it contains no reports.
scan-build: No bugs found.
```

## Expanding our program

You've now seen everything you need to know to use Makefiles. In this last section, I will demonstrate how the build process would change if you wanted to add more C files to your project. We're going to add one more C file and also have our Makefile compile a second binary in addition to `hypot`.

In the spirit of CSE 13S assignment 2, we'll build a test harness that compares the results of our `my_hypot` function with the standard library's `hypot`. The results should be identical, since we're also using the standard library's `sqrt` function and the calculation for what to take the square root of is trivial, but doing this will let us expand on our program.

Here's the code for the test harness. Save it in `hypot-test.c`:

```c
// hypot-test.c
#include <math.h>
#include <stdio.h>

#include "mathlib.h"

int main(void) {
    for (double a = 1.0; a <= 4.0; a += 1.0) {
        for (double b = 1.0; b <= 4.0; b += 1.0) {
            double hypot_result = hypot(a, b), my_hypot_result = my_hypot(a, b),
                   difference = fabs(hypot_result - my_hypot_result);
            printf("a = %.0f, b = %.0f: hypot = %16.15lf, my_hypot = %16.15lf, diff "
                   "= %16.15lf\n",
                   a, b, hypot_result, my_hypot_result, difference);
        }
    }
    return 0;
}

```

We can compile it manually, making sure to link against the math library and our own `mathlib.o` (run `make` again if you don't have the object file):

```
$ clang -Wall -Werror -Wextra -Wpedantic -c hypot-test.c
$ clang -lm -o hypot-test hypot-test.o mathlib.o
$ ./hypot-test
a = 1, b = 1: hypot = 1.414213562373095, my_hypot = 1.414213562373095, diff = 0.000000000000000
a = 1, b = 2: hypot = 2.236067977499790, my_hypot = 2.236067977499790, diff = 0.000000000000000
a = 1, b = 3: hypot = 3.162277660168380, my_hypot = 3.162277660168380, diff = 0.000000000000000
a = 1, b = 4: hypot = 4.123105625617661, my_hypot = 4.123105625617661, diff = 0.000000000000000
a = 2, b = 1: hypot = 2.236067977499790, my_hypot = 2.236067977499790, diff = 0.000000000000000
a = 2, b = 2: hypot = 2.828427124746190, my_hypot = 2.828427124746190, diff = 0.000000000000000
a = 2, b = 3: hypot = 3.605551275463989, my_hypot = 3.605551275463989, diff = 0.000000000000000
a = 2, b = 4: hypot = 4.472135954999580, my_hypot = 4.472135954999580, diff = 0.000000000000000
a = 3, b = 1: hypot = 3.162277660168380, my_hypot = 3.162277660168380, diff = 0.000000000000000
a = 3, b = 2: hypot = 3.605551275463989, my_hypot = 3.605551275463989, diff = 0.000000000000000
a = 3, b = 3: hypot = 4.242640687119285, my_hypot = 4.242640687119285, diff = 0.000000000000000
a = 3, b = 4: hypot = 5.000000000000000, my_hypot = 5.000000000000000, diff = 0.000000000000000
a = 4, b = 1: hypot = 4.123105625617661, my_hypot = 4.123105625617661, diff = 0.000000000000000
a = 4, b = 2: hypot = 4.472135954999580, my_hypot = 4.472135954999580, diff = 0.000000000000000
a = 4, b = 3: hypot = 5.000000000000000, my_hypot = 5.000000000000000, diff = 0.000000000000000
a = 4, b = 4: hypot = 5.656854249492381, my_hypot = 5.656854249492381, diff = 0.000000000000000
```

Next, let's modify our Makefile to automatically build `hypot-test`. First, we'll rename the existing `OBJS` to `HYPOT_OBJS`, since we'll eventually create a new list of object files that are needed for `hypot-test`. We'll also remove the `EXEC` variable and instead write `hypot` directly:

```makefile
CC = clang
CFLAGS = -Wall -Wextra -Werror -Wpedantic
LDFLAGS = -lm
HYPOT_OBJS = hypot.o mathlib.o

all: hypot

hypot: $(HYPOT_OBJS)
	$(CC) $(LDFLAGS) -o hypot $(HYPOT_OBJS)

%.o: %.c
	$(CC) $(CFLAGS) -c $<

clean:
	rm -f hypot $(HYPOT_OBJS)

format:
	clang-format -i -style=file *.[ch]

scan-build: clean
	scan-build --use-cc=$(CC) make
```

Now we can add `HYPOT_TEST_OBJS` with the object files that this program needs, as well as a `hypot-test` target. We'll also add `hypot-test` as a dependency of the `all` target, so that running `make` with no arguments builds both `hypot` and `hypot-test`. And finally, we'll add the executable and object files to our `clean` target:

```makefile
CC = clang
CFLAGS = -Wall -Wextra -Werror -Wpedantic
LDFLAGS = -lm
HYPOT_OBJS = hypot.o mathlib.o
HYPOT_TEST_OBJS = hypot-test.o mathlib.o

all: hypot hypot-test

hypot: $(HYPOT_OBJS)
	$(CC) $(LDFLAGS) -o hypot $(HYPOT_OBJS)

hypot-test: $(HYPOT_TEST_OBJS)
	$(CC) $(LDFLAGS) -o hypot-test $(HYPOT_TEST_OBJS)

%.o: %.c
	$(CC) $(CFLAGS) -c $<

clean:
	rm -f hypot hypot-test $(HYPOT_OBJS) $(HYPOT_TEST_OBJS)

format:
	clang-format -i -style=file *.[ch]

scan-build: clean
	scan-build --use-cc=$(CC) make
```

Let's test this out by running `make clean` and then having it recompile everything with `make`:

```
$ ls
hypot    hypot.o     hypot-test.c  Makefile   mathlib.h
hypot.c  hypot-test  hypot-test.o  mathlib.c  mathlib.o
$ make clean
rm -f hypot hypot-test hypot.o mathlib.o hypot-test.o mathlib.o
$ ls
hypot.c  hypot-test.c  Makefile  mathlib.c  mathlib.h
$ make
clang -Wall -Wextra -Werror -Wpedantic -c hypot.c
clang -Wall -Wextra -Werror -Wpedantic -c mathlib.c
clang -Wall -Wextra -Werror -Wpedantic -c hypot-test.c
clang -lm -o hypot hypot.o mathlib.o
clang -lm -o hypot-test hypot-test.o mathlib.o
$ ls
hypot    hypot.o     hypot-test.c  Makefile   mathlib.h
hypot.c  hypot-test  hypot-test.o  mathlib.c  mathlib.o
$ ./hypot
side a: 3
side b: 4
c = 5.000000
$ ./hypot-test
a = 1, b = 1: hypot = 1.414213562373095, my_hypot = 1.414213562373095, diff = 0.000000000000000
a = 1, b = 2: hypot = 2.236067977499790, my_hypot = 2.236067977499790, diff = 0.000000000000000
a = 1, b = 3: hypot = 3.162277660168380, my_hypot = 3.162277660168380, diff = 0.000000000000000
a = 1, b = 4: hypot = 4.123105625617661, my_hypot = 4.123105625617661, diff = 0.000000000000000
a = 2, b = 1: hypot = 2.236067977499790, my_hypot = 2.236067977499790, diff = 0.000000000000000
a = 2, b = 2: hypot = 2.828427124746190, my_hypot = 2.828427124746190, diff = 0.000000000000000
a = 2, b = 3: hypot = 3.605551275463989, my_hypot = 3.605551275463989, diff = 0.000000000000000
a = 2, b = 4: hypot = 4.472135954999580, my_hypot = 4.472135954999580, diff = 0.000000000000000
a = 3, b = 1: hypot = 3.162277660168380, my_hypot = 3.162277660168380, diff = 0.000000000000000
a = 3, b = 2: hypot = 3.605551275463989, my_hypot = 3.605551275463989, diff = 0.000000000000000
a = 3, b = 3: hypot = 4.242640687119285, my_hypot = 4.242640687119285, diff = 0.000000000000000
a = 3, b = 4: hypot = 5.000000000000000, my_hypot = 5.000000000000000, diff = 0.000000000000000
a = 4, b = 1: hypot = 4.123105625617661, my_hypot = 4.123105625617661, diff = 0.000000000000000
a = 4, b = 2: hypot = 4.472135954999580, my_hypot = 4.472135954999580, diff = 0.000000000000000
a = 4, b = 3: hypot = 5.000000000000000, my_hypot = 5.000000000000000, diff = 0.000000000000000
a = 4, b = 4: hypot = 5.656854249492381, my_hypot = 5.656854249492381, diff = 0.000000000000000
```

It all worked! Make handles building multiple binaries very well—notice how it only built `mathlib.c` once, even though it is needed by both binaries. Also, this Makefile compiles both binaries by default (thanks to the `all` target), but you can also compile only one binary with `make hypot` or `make hypot-test`.
