---
title: "Data Types and Variables"
linkTitle: "Data Types and Variables"
author: "Brian Mak"
date: "2021-09-11"
weight: 1
icon:
draft: false
description: >
  An explanation of data types and variables in C.
---

## What are data types

Data types are a way to classify a variable or piece of data. Examples of common data types in some programming languages are integers, floats, characters, and strings.

## How data types work in C

C is a strongly-typed and statically-typed language. In a strongly-typed language, each variable will have a data type associated with it. In a statically-typed language, each variable must have a defined data type at compile-time that cannot change. This means that variables' data types must be explicitly defined in your code.

Usage of data types will be covered in the "Variables" section. An example of a variable declaration and definition in C is shown below:

```c
int myInteger = 0;
```

## Comparison of type system in C and in other languages

C's type system is similar to Java's and C#'s type system in that they are both strongly-typed and statically-typed languages. In Java and C#, a variable would be declared and defined as such:

```java
int myInteger = 0;
```

You'll notice that Java, C#, and C are similar in the way they declare and define their variables.

However, C's type system is different from Python's type system. Python is a strongly-typed and dynamically-typed language. In a dynamically-typed language, the usage of variable types is checked at run-time. This means that the data type of a variable can change at run-time, and is not bound to one specific type. In Python, a variable would be declared and defined as such:

```python
myInteger = 0
```

You'll notice that in Python, the data type of variables is not explicitly defined in the code. Instead, it will be inferred at run-time.

## C's built-in data types

C has a handful of built-in data types. Some of the basic types built into C are ``char``, ``short``, ``int``, ``long``, ``float``, and ``double``.

You'll notice that C does not have a type for strings (a sequence of characters), like many other programming languages. This is because strings are really just a sequence of characters. In C, strings are represented with ``char[]``, or in other words, an array of characters. An array in C is a data structure containing one or more elements of a single data type, laid out in contiguous memory.

You'll also notice that C does not have a built-in type for booleans (true/false) by default, like many other programming languages. Booleans in C are represented with ``int``s. Zero is false, and any non-zero value is true. // TO-DO: Mention stdbool.

Another thing to be aware of about data types in C is that none of them have a set size or range. Instead, C makes certain guarantees about sizes and ranges. The actual size or range of data types is left up to the specific implementation of C. More information about these guarantees can be found [here](https://en.wikipedia.org/wiki/C_data_types#Main_types) and in the C standard.

## Additional resources

Data types - https://www.destroyallsoftware.com/compendium/types?share_key=baf6b67369843fa2

Data types in C - https://en.wikipedia.org/wiki/C_data_types
