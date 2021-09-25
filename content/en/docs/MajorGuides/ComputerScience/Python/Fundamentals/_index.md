---
title: "Python Guide Pt.1"
linkTitle: "Python Guide Pt.1"
author: "James Zhou"
date: "2021-09-22"
weight: 1
icon:
draft: false
description: >
  Part 1 of a comprehensive guide covering an introduction to python curtailed towards the curriculum of CSE20 and CSE30. This part will cover the fundamentals and basics of python.
---

# Python Guide Part 1

## Table of Contents

- [Python Guide Part 1](#python-guide-part-1)
  - [Table of Contents](#table-of-contents)
- [1. Getting into Programming](#1-getting-into-programming)
  - [1.1 What is programming?](#11-what-is-programming)
  - [1.2 Python](#12-python)
  - [1.3 Using the internet](#13-using-the-internet)
  - [1.4 Getting started](#14-getting-started)
- [2. Your first program](#2-your-first-program)
- [3. Variables, data types, and operators](#3-variables-data-types-and-operators)
- [4. Loops](#4-loops)
  - [4.1 If loops](#41-if-loops)
  - [4.2 While loops](#42-while-loops)
  - [4.3 For loops](#43-for-loops)
  - [4.4 List iteration](#44-list-iteration)
  - [4.4 Nested loops](#44-nested-loops)
- [5. Conclusion](#5-conclusion)

# 1. Getting into Programming

## 1.1 What is programming?

Programming is the process or activity of writing computer programs. Another way to view programming is the act of creating "things" that the computer can understand and execute. What you will be doing in your upcoming courses is writing computer programs in the language known as python.

## 1.2 Python

Python is an interpreted high-level general-purpose programming language. Interpreted means that the language does not to be compiled before running (unlike C++ or C, for example). High-level means that it is easier for the human to read and understand compared to the 1's and 0's computers see. Python's design philosophy emphasizes code readability with its use of significant indentation. Its language architecture in combination with its object-oriented approach aims to help programmers write clear, logical code for small and large-scale projects. In other words, it's a great language for new programmers!

## 1.3 Using the internet

When first starting programming, you might come across a lot of different terms that you're unfamiliar with. An important lesson to learn early on is that Google is your friend. If there's anything you're confused about, just look it up and there will be an explanation out there. Just be careful with looking up solutions for your labs because that's against course policy and can result in academic dishonesty violations.

## 1.4 Getting started

Your course instructor will probably have a section on getting started but here's what you should do in case you want to get a head start:

1. install the latest version of python
2. download the IDE (integrated development environment) or text editor of your choice
3. create a .py file with your name of choice
4. open said file from step 3 in your text editor or IDE and start coding!

# 2. Your first program

It's common practice for the first program you make to be a simple one. Print is used to print things to the console in python. Try to print your name and age to the console as your first program!

Code:

```python
print("my name is James Zhou and I'm 19 years old")
```

Output:\
my name is James Zhou and I'm 19 years old

# 3. Variables, data types, and operators

One thing you might have noticed when making your first program is that to print out your name and age, the arguments inside the print needed to be wrapped in quotation marks. This is because your name is most likely a string, which is a data type. Python has several built-in data types but the ones you will use the most are:

1. int (integers)\
   These numbers respresent integers, like on a number line.

```python
x = 1
y = 3
```

2. float\
   Floats are decimal representations of numbers.

```
float_pi = 3.1415
balance = 103.23
```

3. char (character)\
   Chars are characters, like 'a', 'b', and 'c'. Unlike other programming languages, chars are just strings with single letters stored inside but it's a good term to use for future classes.

```python
firstInitial = 'J'
lastInitial = 'Z'
```

4. str (strings)\
   Strings are arrays of chars that form comprehensible (or incomprehensible) words and sentences.

```python
firstName = "James"
lastName = "Zhou"
```

5. list\
   Lists are arrays of different objects. The cool thing about python is that arrays can hold different objects unlike other languages which makes complex programs a lot easier.

```python
friends = ["Isaac", "Brian", "Brent", "Vincent", "Aaron"]
fruit = ["Apples", 5, "Pears", 10]
```

6. tuple\
   Tuples in their most basic form are just immutable lists (lists that can't be changed) with parantheses instead of brackets.

```python
coord1 = (0,0)
coord2 = (3,0)
coord3 = (0,4)
```

7. set\
   Sets might seem like lists, but they are very different. First, they use curley braces instead. Additionally, they are unordered, unindexed, don't allow duplicates, and immutable.

```python
test_set = {"a", "b", "c"}
```

8. dict (dictionary)\
   Dictionaries are used to store data values in key:value pairs and are useful for finding data quickly instead of searching through an entire list. A dictionary is ordered, changeable, and does not allow duplicates.

```python
car1 = {
  "brand": "Ferrari",
  "model": "SF90 Stradale",
  "year": 2020
}
```

9. bool (boolean)\
   Named after George Boole, booleans hold True or False values.

```python
answer1 = True
answer2 = False
```

# 4. Loops

There are many different loops in python. Here a a few that you'll become familiar with.

## 4.1 If loops

If loops are yes or no loops. If the statement given to the if loop is true, it will execute the if loop. Otherwise, the loop woop won't execute. Else is the opposite of if. If the if loop doesn't execute, then the else loop will execute. If loops can be chained with an elif statement. Here are some examples to help visualize if loops.

```python
if (true):
    print("this loop is executed")

if (false):
    print("this loop is not executed")
print("this still gets printed")

if (false):
    print("this loop is not executed")
else:
    print("this loop is executed")

if (false):
    print("this loop is not executed")
elif (true):
    print("this loop is executed")
else:
    print("this loop is not executed")
```

Here are some examples to test your understanding:

```python
#what is the output?
x = 5
if (x + 5 === 10):
    print(x)
print(x+5)
```

```python
#what is the output?
grade = 95
if (grade < 60):
    print("you got an F")
if (grade > 70):
    print("you got a C")
if (grade > 80):
    print("you got a B")
elif (grade > 90):
    print("you got an A")
else:
    print("please enter a valid grade")
```

## 4.2 While loops

The while loop will execute a set of statements as long as a condition is true. This can potentially lead to infinite loops so be careful when writing the check statement.

```python
i = 0
while(i<10):
    print(i)
    i++
```

```python
#what is the output?
i = 10
counter = 0
while (i > 5):
    counter+=i
print(counter)
```

```python
#what is the output?
i = 1
while (i == 0):
    i++
print(i)
```

## 4.3 For loops

The for loop iterates a set of statements for however many iterations are set when defining the for loop. This can also lead to infinite loops if not careful in setting up definitions.

```python
for x in range(10):
  print(x)
```

```python
for x in range(0,10,2):
    print(x)
```

output:

```python
0
2
4
6
8
```

## 4.4 List iteration

For loops can also be used to iterate through the contents of a list.

```python
names = ["bob", "joe", "harry", "jenny", "rose", "miguel"]
for x in names:
    print(x)
```

output:

```python
bob
joe
harry
jenny
rose
miguel
```

```python
#what is the output?
arr = [1, 2, 3, "a", "c", "hello", 2.34, False, {1,2,3}, [0,-5,3]]
for x in arr:
    print(x)
```

output:

```python
1
2
3
a
c
hello
2.34
False
{1, 2, 3}
[0, -5, 3]
```

## 4.4 Nested loops

In python, loops can be put inside of each other. This results in what's called a "nested loop".

Generally, python flows down the chain of loops so the inner loops always finish running before the outer loop can continue.

```python
for i in range(3):
    for j in range(3):
        print("("+str(i)+","+str(j)+")")
```

output:

```python
(0,0)
(0,1)
(0,2)
(1,0)
(1,1)
(1,2)
(2,0)
(2,1)
(2,2)
```

These loops can take a very long time to execute if the parameters or chaining is long. There are often smarter ways to display or check values so only use this if you have to.

# 5. Conclusion

This concludes the part 1 of the intro to python guide! If you read all the way through, you should be acquainted with the majority of python fundamentals. You should now be ready to take on the more difficult topics in part 2. Feel free to refer back to this guide whenever you need to refresh yourself on any of the fundamentals. Please keep in mind that while this guide is long, it was not designed to cover EVERY topic that comes up in your CS classes. In other words, pay attention still!

CS is a really fun major and I'm sure you'll enjoy the process. Enjoy the content and good luck!
