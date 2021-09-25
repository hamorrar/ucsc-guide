---
title: "Python Guide Pt.2"
linkTitle: "Python Guide Pt.2"
author: "James Zhou"
date: "2021-09-22"
weight: 1
icon:
draft: false
description: >
  Part 2 of a comprehensive guide covering an introduction to python curtailed towards the curriculum of CSE20 and CSE30. This part will cover control flow and intermediate python techniques.
---

# Python Guide Part 2

## Table of Contents

- [Python Guide Part 2](#python-guide-part-2)
  - [Table of Contents](#table-of-contents)
- [1. Control flow](#1-control-flow)
  - [1.1 Break statement](#11-break-statement)
  - [1.2 Continue statement](#12-continue-statement)
  - [1.3 Pass](#13-pass)
- [2. Functions](#2-functions)
  - [2.1 Docstrings](#21-docstrings)
  - [2.2 Return](#22-return)
  - [2.3 Default return and None](#23-default-return-and-none)
- [3. Data structures](#3-data-structures)
  - [3.1 The stack](#31-the-stack)
  - [3.2 The queue](#32-the-queue)
- [4. Strings](#4-strings)
  - [4.1 String operators](#41-string-operators)
  - [4.2 Slicing](#42-slicing)
  - [4.3 String comparison](#43-string-comparison)
    - [Option 1: Using relational operators](#option-1-using-relational-operators)
    - [Option 2: using `is` and `is not`](#option-2-using-is-and-is-not)
  - [4.4 Formatting](#44-formatting)
- [5. Lists cont.](#5-lists-cont)
  - [5.1 Indices](#51-indices)
  - [5.2 List slicing](#52-list-slicing)
  - [5.3 List sorting](#53-list-sorting)
  - [5.4 List comprehension](#54-list-comprehension)
- [6. Conclusion](#6-conclusion)

# 1. Control flow

A program's control flow is the order in which the program's code executes. Generally, the flow of executing statements is linear. For example:

```python
print(1)
print(2)
print(3)
```

Will print:

```python
1
2
3
```

As you can see, the execution of the print statements happens linearly.

The control flow of a Python program is regulated by conditional statements, loops, and function calls. Using these can be useful if you want the computer to jump between lines of code, functions, and applications.

## 1.1 Break statement

The break statement in python terminates the current loop that's being run and resumes execution at the next statement.

The most common use for a break statement is when some external condition occurs requiring a quick exit from a loop that would normally run until its condition is fulfilled.

When using nested loops, the break statement stops the execution of the innermost loop and starts executing the next line of code after the block. Here are some examples to help visualize a break statement:

```python
for i in range(100):
    if i == 3:
        break
print('Current number :', i)
```

Output:

```python
Current number : 3
```

As you can see, the innermost loop is exited but the next line of code after the block is then executed, thus canceling the "outer" for loop. There are many more cases in which breaks can be used but I'll let your CS classes teach you those.

## 1.2 Continue statement

The continue statement sets the control flow back to the beginning of a loop. The continue statement does not execute all the remaining statements in the current iteration of the loop. Think of it as going directly to Go in Monopoly.

```python
for i in range(3):
    if i == 2:
        continue
    print("num ", i)
```

Output:

```python
num  0
num  1
```

The example above shows how when i == 2, the continue statement gets triggered, skipping the print statement.

## 1.3 Pass

Pass is a simple placeholder statement or null statement that does not do anything. It's similar to white space but the computer does recognize it. The syntax is just "pass".

# 2. Functions

Functions are a block of code that only runs when the function itself is called. Data, known as parameters, can be passed into a function which can then be operated on. A function can return data as a result which can then in turn feed into other functions.

Functions can range from simple modularization of code to complex algorithms. I'll keep it simple for now though and just show the syntax.

In your future courses, you will become well acquainted with the versatility and variety of functions.

```python
'''
definition of a function
the def is important as it distinguises it to the computer that a function is ahead
parameters go inside the parantheses, which can then be used inside the function
'''
def printName(firstName, lastName):
    print("Hello,", firstName, lastName)

'''
calling functions is simple
'''
printName("James","Zhou")
```

Output:

```python
Hello, James Zhou
```

Here is an example using return, which will be covered in more detail later.

```python
def getSum(x,y):
    return x+y
print(getSum(10,10))
```

Output:

```python
20
```

## 2.1 Docstrings

Python docstrings are string literals that appear right after the definition of a function, method, class, or module. These are used to inform the coder(s) what the function/purpose of your code is. They are slightly different from comments in that using the ` __doc__` attribute, you can access the string literal.

Here's an example:

```python
def getSum(x,y):
    '''this function returns the sum of 2 numbers'''
    return x+y
print(getSum.__doc__)
```

Output:

```python
this function returns the sum of 2 numbers
```

## 2.2 Return

The `return` keyword is to exit a function and return a value. This can be useful for control flow as well as retrieving data for later use.

```python
def longProgram():
    for i in range(1000000):
        if i == 10:
            return i
print(longProgram())
```

Output:

```python
10
```

Another example:

```python
def pythag(a,b):
    answer = getSum(exponent(a,2), exponent(b,2))
    answer = exponent(answer, 1/2)
    return answer

def getSum(a,b):
    return a+b

def exponent(a,b):
    return a**b

print(pythag(3,4))
```

Output:

```python
5.0
```

## 2.3 Default return and None

The default return is always None in python. If a return statement is left empty, then None is returned as default. This can be useful if you want to exit a function entirely at a certain point.

```python
def test():
    return
print(test())
```

Output:

```
None
```

None is pretty self-explanitory; it holds no value.

# 3. Data structures

The two data structures you will encounter in your early CS classes are the stack and the queue.

## 3.1 The stack

The stack is a linear data structure that stores items in a Last-In/First-Out (LIFO) or First-In/Last-Out (FILO) style. In a stack, a new element is added at one end and an element is removed from that end only. The insert and delete operations are often called push and pop.

The analogy professors usually use is a stack of plates. It's impossible to remove the bottom plate once the stack starts growing so the only way to get to the bottom is to remove all the new plates before getting to the last plate, hence the name FILO.

Stacks are usually built with lists due to their mutability.

There are several functions built into python that are associated with stacks:

```python
empty() #Returns whether the stack is empty
size() #Returns the size of the stack
top() #Returns a reference to the topmost element of the stack
push(a) #Inserts the element ‘a’ at the top of the stack
pop() #Deletes the topmost element of the stack
```

## 3.2 The queue

Like a stack, the queue is a linear data structure that stores items in but in a First In First Out (FIFO) manner.

With a queue the newest added item is removed first.

A good analogy of a queue is like a queue of diners waiting to enter the dining hall. Whoever gets there first, gets to go in first.

Several functions are associated with queues (not built-in):

```python
Enqueue: # Adds an item to the queue. If the queue is full, then it is said to be an Overflow condition
Dequeue: # Removes an item from the queue. The items are popped in the same order in which they are pushed. If the queue is empty, then it is said to be an Underflow condition
Front: # Get the front item from queue
Rear: # Get the last item from queue
```

# 4. Strings

Strings might seem pretty simple but there are a lot of tricks and caveats to them which will be summarized in this chapter.

## 4.1 String operators

Python has several built-in string operators that make operating on strings much easier. Since everything in python is an object, to access the string operators, just attach the function to the end of a string of your choice.

Here is a good resource for the different string methods:\
https://www.w3schools.com/python/python_ref_string.asp

You probably won't use them all but it's good to know some common ones like `capitalize()` , `casefold() ` , `count()` , `split()` etc.

Here's an example of capitalizing the first letter of each word and returning the string for later use:

```python
sentence = "the quick brown fox jumped over the river"
wordList = []
for word in sentence.split():
    wordList.append(word.capitalize())
print(wordList)
```

Output:

```python
['The', 'Quick', 'Brown', 'Fox', 'Jumped', 'Over', 'The', 'River']
```

## 4.2 Slicing

Slicing is one of the most frequently used operations on lists and tuples (strings are basically char arrays). As the name implies, slicing takes a "slice" and returns it for later use.

Here is an example of slicing in action:

```python
sentence = "Python is fun"
sentenceSlice = slice(3, 5)
print(sentence[sentenceSlice])
```

Output:

```python
ho
```

sentenceSlice is declared as a slice object from index 3 to index 5 excluding index 5. The string `"Python is fun"` has `Pyt` for indicies 0-2. `ho` is then printed because those are the only 2 chars in the selected slice.

To really make it clear, here is the syntax:

```python
randomSliceObject = slice(start, end, step)
```

Step means how many chars to skip before including the next char in the slice. The default step is 1. Slicing can be done without the declaration of a slice object but we'll talk about that more when we cover lists in more detail.

## 4.3 String comparison

Strings like other objects, can be compared in python. There are a few options to choose from. I'll go over the 2 easiest methods here.

### Option 1: Using relational operators

```python
string1 = "hello"
string2 = "Hello"

print(string1 < string2)
print(string1 <= string2)
print(string1 > string2)
print(string1 >= string2)
print(string1 == string2)
print(string1 != string2)
```

Output:

```python
False
False
True
True
False
True
```

This words by comparing the Ascii values of each character and seeing if they are greater or less than each other. `h` has a value of 104 while `H` has a value of 72. With the rest of the letters being the same, we can see why we get the results above.

### Option 2: using `is` and `is not`

This method uses hex values to check if the string IDs are the same for each string object. It's a pretty interesting topic that your CS classes will probably go over. It's similar to the == operation but it doesn't take into account mutability. If a string is changed and it's compared with `is` to another string with the same contents, the returned value will still be false.

Example:

```python
string1 = "hello"
string2 = "hellos"
string1 += "s"
print(string1)
print(string2)
print(string1 == string2)
print(string1 is string2)
```

Output:

```python
hellos
hellos
True
False
```

## 4.4 Formatting

Formatting strings isn't super complicated. To be honest, I haven't memorized all of the different methods just because you can always pull them up whenever you need them. Here's a good resource if you need a specific formatting tool:

https://www.w3schools.com/python/ref_string_format.asp

The syntax is the same for each method. Here's an example of 2 digit floating point, thousand split syntax:

```python
balance = 1234567.890000001
txt = "{0} {1}'s balance: ${2:+.2f}".format("James", "Zhou", balance)
print(txt)
```

Output:

```
James Zhou's balance: $+1234567.89
```

# 5. Lists cont.

We briefly glossed over the syntax and functionalities of lists earlier but let's delve a little deeper. Lists are one of the most important data structures that can be scaled to huge scales so having a good understanding of their intricacies is imperative.

## 5.1 Indices

List indices help address where each item of the list is located. Indices can also be the source of frustration and headache when working with lists due to the numerous bugs you can encounter. One of the most common bugs for new programmers is the index out-of-bounds error. This occurs when your program tries to access something outside of the bounds of an array.

Here's an example:

```python
list1 = [1,2,3]
print(list1[3])
```

Output:

```
IndexError: list index out of range
```

To avoid this, make sure your loops' parameters are properly defined to avoid making excessive iterations.

## 5.2 List slicing

Lists, like strings, can also be sliced. The syntax can be much shorter without even needing to declare a slice object. Here's an example:

```python
randomList = [1,2,3,4,5,6,7,8,9,10]
randomList = randomList[0:9:2]
print(randomList)
```

Output:

```
[1, 3, 5, 7, 9]
```

The syntax is as follows:

```python
randomList[ start : end : step ]
```

Slicing can also be done backwards using negative numbers. Try to guess what this output will be:

```python
randomList = [1,2,3,4,5,6,7,8,9,10]
randomList = randomList[9:0:-2]
print(randomList)
```

Output:

```
[10, 8, 6, 4, 2]
```

## 5.3 List sorting

Lists can be sorted in python using the built-in `sort()` method. The built-in method uses TimSort, which is a merge of insertion and merge sort. You'll learn all about that stuff later but just know that it's pretty efficient and will serve your purposes.

Here's the syntax for ascending order:

```python
list1.sort()
```

Here's the syntax for descending order:

```python
list1.sort(reverse=True)
```

A key can also be inserted as a parameter to specify how you want the list to be sorted. Here's an example of sorting a list based on the value of the 2nd element instead of value:

```python
list1 = [(0,0),(1,0),(2,0),(1,10)]
list1.sort()
print(list1)

def getSecond(tupleX):
    return tupleX[1]

list1.sort(key=getSecond)
print(list1)
```

Output:

```
[(0, 0), (1, 0), (1, 10), (2, 0)]
[(0, 0), (1, 0), (2, 0), (1, 10)]
```

## 5.4 List comprehension

List comprehension is a shorter way to create new lists based on the values of an existing list. This is useful to save time and when working with multiple, larger lists, requiring multiple loops.

Here's an example for creating a new list while preserving the old one without list comprehension:

```python
names = ["James", "Bob", "Charlie", "Dom", "Ethan"]
newlist = []

for x in names:
  if len(x) < 6:
    newlist.append(x)

print(newlist)
```

Output:

```
['James', 'Bob', 'Dom', 'Ethan']
```

With list comprehension:

```python
names = ["James", "Bob", "Charlie", "Dom", "Ethan"]
newlist = [x for x in names if(len(x) < 6)]
print(newlist)
```

Output:

```
['James', 'Bob', 'Dom', 'Ethan']
```

Here's the syntax:

```python
newlist = [expression for item in iterable if(condition)]
```

# 6. Conclusion

This concludes the part 2 of the intro to python guide! If you read all the way through, you should be acquainted with the majority of intermediate python topics. You should now be ready to take on the more advanced topics in part 3. Feel free to refer back to this guide whenever you need to refresh yourself on any of the fundamentals. Please keep in mind that while this guide is long, it was not designed to cover EVERY topic that comes up in your CS classes. In other words, pay attention still!

CS is a really fun major and I'm sure you'll enjoy the process. Enjoy the content and good luck!
