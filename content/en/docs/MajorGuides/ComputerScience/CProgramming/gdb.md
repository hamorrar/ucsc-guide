---
title: "Debugging with GDB"
linkTitle: "GDB"
author: "Miles Glapa-Grossklag"
date: 2021-10-13T00:00:00-07:00
weight: 1
icon:
draft: false
description: Debugging with GDB to identify segmentation faults.
---
# Prerequisites

* Compile with debug symbols. To do this, add the `-g` flag when you compile.
  For example, `clang -g -o program.o program.c`. For convenience, add a target
  to your makefile, i.e.:

  ```makefile
  debug: CFLAGS += -g
  debug: all
  ```
* Launch GDB using `./gdb --args` followed by the your normal method of
  execution. For example, for a program named *program* and one flag *--flag*,
  run `gdb --args ./program --flags`.
* Once inside GDB, the command `run` will run your program.

# Finding Segmentation Faults

First, run your program using GDB. When your program crashes, you should see
the exact line on which your program failed.

For more information, use the `backtrace` command. The stack trace should show
the path your program took during its execution. For example, if your program
crashes in the standard library's `strlen` function, there won't be much
information there. Running `backtrace` will show you the arguments passed to
the function and which function called `strlen`.

# Example

```
$ gdb --args ./executable
Reading symbols from ./executable...
```

GDB has read the executable. The `(gdb)` prompt means anything typed is sent to
GDB, not to the shell.

```
(gdb) run
Starting program: /path/to/executable

Program received signal SIGSEGV, Segmentation fault.
0x000055555555512c in my_function (array=0x0) at ./segfault.c:4
4       return array[0];
```

The program received a segmentation fault in the function `my_function`.  The
function has one argument, `array=0x0` (i.e., NULL).This is the source of the
segmentation fault, since the code is attempting to access the 0th element of
NULL memory.

```
(gdb) backtrace
#0  0x000055555555512c in my_function (array=0x0) at ./segfault.c:4
#1  0x0000555555555150 in main () at ./segfault.c:9
(gdb)
```

The function `my_function` was called from the function `main`.
