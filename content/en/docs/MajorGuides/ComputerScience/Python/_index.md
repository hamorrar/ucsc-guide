---
title: "Python Guide"
linkTitle: "Python Guide"
author: "James Zhou"
date: "2021-09-22"
weight: 1
icon:
draft: false
description: >
  A comprehensive guide covering an introduction to python curtailed towards the curriculum of CSE20 and CSE30.
---
# Introduction to Python

## Table of Contents

- [Introduction to Python](#introduction-to-python)
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
- [5. Control flow](#5-control-flow)
  - [5.1 Break statement](#51-break-statement)
  - [5.2 Continue statement](#52-continue-statement)
  - [5.3 Pass](#53-pass)
- [6. Functions](#6-functions)
  - [6.1 Docstrings](#61-docstrings)
  - [6.2 Return](#62-return)
  - [6.3 Default return and None](#63-default-return-and-none)
- [7. Data structures](#7-data-structures)
  - [7.1 The stack](#71-the-stack)
  - [7.2 The queue](#72-the-queue)
- [8. Strings](#8-strings)
  - [8.1 String operators](#81-string-operators)
  - [8.2 Slicing](#82-slicing)
  - [8.3 String comparison](#83-string-comparison)
    - [Option 1: Using relational operators](#option-1-using-relational-operators)
    - [Option 2: using `is` and `is not`](#option-2-using-is-and-is-not)
  - [8.4 Formatting](#84-formatting)
- [9. Lists cont.](#9-lists-cont)
  - [9.1 Indices](#91-indices)
  - [9.2 List slicing](#92-list-slicing)
  - [9.3 List sorting](#93-list-sorting)
  - [9.4 List comprehension](#94-list-comprehension)
- [10. Generators](#10-generators)
- [11. Dictionaries cont.](#11-dictionaries-cont)
- [12. Classes and objects](#12-classes-and-objects)
  - [12.1 Classes](#121-classes)
  - [12.2 Objects](#122-objects)
  - [12.3 More complex classes](#123-more-complex-classes)
  - [12.4 Inheritance](#124-inheritance)
  - [12.5 Inheritance vs composition](#125-inheritance-vs-composition)
- [13. Recursion](#13-recursion)
- [14. Conclusion](#14-conclusion)

# 1. Getting into Programming

## 1.1 What is programming?

Programming is the process or activity of writing computer programs. Another way to think of programming is creating "things" that the computer can understand and execute. What you will be doing in your upcoming courses is writing computer programs in the language known as python.

## 1.2 Python

Python is an interpreted high-level general-purpose programming language. Interpreted means that the language does not to be compiled before running (unlike C++ or C for example). High-level means that it's easier for the human to read and understand compared to the 1's and 0's computers see. Python's design philosophy emphasizes code readability with its use of significant indentation. Its language constructs as well as its object-oriented approach aim to help programmers write clear, logical code for small and large-scale projects. In other words, it's a great language for new programmers!

## 1.3 Using the internet

When first starting programming, you might come across a lot of different terms that you're unfamiliar with. An important lesson to learn early on is that Google is your friend. If there's anything you're confused about, just look it up and there will be an explanation out there. Just be careful with looking up solutions for your labs because that's against course policy and can result in academic dishonety violations.

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

One thing you might have noticed when making your first program is that in order to print out your name and age, the arguments inside the print needed to be wrapped in quotation marks. This is because your name is most likely a string, which is a data type. Python has several built-in data types but the ones you will use the most are:

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

If loops are yes or no loops. If the statement given to the if loop is true, it will execute the if loop. Otherwise, the loop woop won't execute. Else is the opposite of if. If the if loop doesn't execute, then the else loop will execute. If loops can be chained with an if else statement. Here are some examples to help visualize if loops.

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
else if (true):
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
else if (grade > 90):
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

# 5. Control flow

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

As you can see, the execution of the print statements happens linearlly.

The control flow of a Python program is regulated by conditional statements, loops, and function calls. Using these can be useful if you want the computer to jump between lines of code, functions, and applications.

## 5.1 Break statement

The break statement in python terminates the current loop and being run and resumes execution at the next statement.

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

As you can see, the innermost loop is exited but the next line of code after the block is then executed, thus cancelling the "outer" for loop. There are many more cases in which breaks can be used but I'll let your CS classes teach you those.

## 5.2 Continue statement

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

## 5.3 Pass

Pass is a simple place holder statement or null statement that does not do anything. It's similar to white space but the computer does recognize it. The syntax is just "pass".

# 6. Functions

Functions are a block of code which only runs when the function itself is called. Data, known as parameters, can be passed into a function which can then be operated on. A function can return data as a result which can then in turn feed into other functions.

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

## 6.1 Docstrings

Python docstrings are string literals that appear right after the definition of a function, method, class, or module. These are used to inform the coder(s) what the function/purpose of your code is. They are slighlty different from comments in that using the ` __doc__` attribute, you can access the string literal.

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

## 6.2 Return

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

## 6.3 Default return and None

The default return is always None in python. If a return statement is left empty, than None is returned as default. This can be useful if you want to exit a function entirely at a certain point.

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

# 7. Data structures

The two data structures you will encounter in your early CS classes are the stack and the queue.

## 7.1 The stack

The stack is a linear data structure that stores items in a Last-In/First-Out (LIFO) or First-In/Last-Out (FILO) style. In a stack, a new element is added at one end and an element is removed from that end only. The insert and delete operations are often called push and pop.

The analogy professors usually use is a stack of plates. It's impossible to remove the bottom plate once the stack starts growing so the only way to get to the bottom is to remove all the new plates before getting to the last plate, hence the name FILO.

Stacks are usually built with lists due to their mutability.

There are several functions built-into python that are associated with stacks:

```python
empty() #Returns whether the stack is empty
size() #Returns the size of the stack
top() #Returns a reference to the topmost element of the stack
push(a) #Inserts the element ‘a’ at the top of the stack
pop() #Deletes the topmost element of the stack
```

## 7.2 The queue

Like a stack, the queue is a linear data structure that stores items in but in a First In First Out (FIFO) manner.

With a queue the newest added item is removed first.

A good analogy of a queue is like a queue of diners waiting to enter the dining hall. Whoever gets there first, gets to go in first.

There are several functions that are associated with queues (not built-in):

```python
Enqueue: # Adds an item to the queue. If the queue is full, then it is said to be an Overflow condition
Dequeue: # Removes an item from the queue. The items are popped in the same order in which they are pushed. If the queue is empty, then it is said to be an Underflow condition
Front: # Get the front item from queue
Rear: # Get the last item from queue
```

# 8. Strings

Strings might seem pretty simple but there are a lot of tricks and caveats to them which will be summarized in this chapter.

## 8.1 String operators

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

## 8.2 Slicing

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

## 8.3 String comparison

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

## 8.4 Formatting

Formatting strings isn't super complicated. To be honest, I haven't memorized all of the different methods just because you can always pull them up whenever you need. Here's a good resource if you need a specific formatting tool:

https://www.w3schools.com/python/ref_string_format.asp

The syntax is the same for each method. Here's an example of negative, 2 digit floating point, thousand split syntax:

```python
balance = 1234567.890000001
txt = "{0} {1}'s balance: ${2:+.2f}".format("James", "Zhou", balance)
print(txt)
```

Output:

```
James Zhou's balance: $+1234567.89
```

# 9. Lists cont.

We briefly glossed over the syntax and functionalities of lists earlier but let's delve a little deeper. Lists are one of the most important data structures that can be scaled to huge scales so having a good understanding of their intricacies is imperative.

## 9.1 Indices

List indices help address where each item of the list is located. Indices can also be the source of frustration and head ache when working with lists due to the numerous bugs you can encounter. One of the most common bugs for new programmers is the index out of bounds error. This occurs when your program tries to access something outside of the bounds of an array.

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

## 9.2 List slicing

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

## 9.3 List sorting

Lists can be sorted in python using the built in `sort()` method. The built-in method uses TimSort, which is a merge of insertion and merge sort. You'll learn all about that stuff later but just know that it's pretty efficient and will serve your purposes.

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

## 9.4 List comprehension

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

# 10. Generators

Generators generate values for use. They don't require a lot of code to get running. The defining characteristic of a generator is the use of the keyword `yield`. `yield` statements behave similarly to return in that they return a value. The similarities stop there though. Unlike how return exits the function as soon as it finishes executing, yield allows the function block to continue firing. You'll learn a lot more about them in your upcoming CS classes but here is a simple example of a generator:

```python
def fib(iterations):
    a, b = 0, 1
    while a < iterations:
        yield a
        a, b = b, a + b

x = fib(5)

print(x.__next__())
print(x.__next__())
print(x.__next__())
print(x.__next__())
print(x.__next__())
```

Output:

```
0
1
1
2
3
```

Here's a challenge for you. Try to create a generator for prime numbers and print out the first 100 iterations.

# 11. Dictionaries cont.

Dictionaries in python can be a useful tool for sorting data. Dictionaries can't store duplicates and every key needs to be unique, making them a great resource for mapping unique objects.

There are several different types of implementations of dictionaries such as hast tables and red-black trees but I'll let your CS classes explain those concepts.

Dictionaries can store different object and data types inside of them. Dictionaries can also be nested inside of each other. For example:

```python
person1 = {
  "fName": "John",
  "lName": "Doe",
  "age": 27,
  "hobbies": ["coding", "watching TV", "eating"],
  "car" : {
      "brand": "Ford",
      "model": "Mustang",
      "year": 1990
  }
}

print(person1)
print(person1["car"])
print(person1["car"]["brand"])
```

Output:

```
{'fName': 'John', 'lName': 'Doe', 'age': 27, 'hobbies': ['coding', 'watching TV', 'eating'], 'car': {'brand': 'Ford', 'model': 'Mustang', 'year': 1990}}
{'brand': 'Ford', 'model': 'Mustang', 'year': 1990}
Ford
```

There are a lot of ways to use dictionaries. Be creative with their implementation and you'll be surprised at how useful they can be.

# 12. Classes and objects

Python is an object oriented programming language, meaning that everything inside of python is an object (besides control flow). This chapter will cover what objects are and the classes that define different objects.

## 12.1 Classes

Classes in python serve as object blueprints. They detail what an object consists of --- its characteristics if you will. Similarly to how we classify certain animals under specific classes (domains), we can do the same with objects. Let's look at the basic syntax of creating our own python class:

```python
class human:
    name = "Joe"
    age = 0
    gender = "Male"
```

This is our very own human class. Let's next look over how to make an object of class human.

## 12.2 Objects

Using the syntax from above, we can create an object of class human like so:

```python
class human:
    name = "Joe"
    age = 0
    gender = "Male"

human1 = human()
print(human1.name)
print(human1.age)
print(human1.gender)
```

Output:

```python
Joe
0
Male
```

Unfortunately, every human object we ever create will always have the name of Joe, an age of 0, and be male. Not a particularly useful class as humans come in all varieties. As you can see though, we can access the data of an object using the same approach we used with lists and strings. This is because lists and strings are also objects, just of different classes.

## 12.3 More complex classes

To make dynamic objects, we need to have flexibility with our class constructors. Here's how to add parameters, or constructors, to a python class using the function `__init()__`:

```python
class human():
    def __init__(self, fName, lName, age, gender):
        self.fName = fName
        self.lName = lName
        self.age = age
        self.gender = gender
```

Now, when we create a new human object, we can add some uniqueness to it. Using the `__init__()` function allows us to initialize an object using set parameters that the user can input. We always include self as the first parameter because we need to address the object itself when first initializing the arguments we pass to the constructor. We can add more functions using `def` but I'll let you expiriment with that yourself.

```python
human2 = human("James", "Zhou", 19, "Male")
print(human2.fName)
print(human2.lName)
print(human2.age)
print(human2.gender)
```

Output:

```
James
Zhou
19
Male
```

Finally, object values can be modified.

```python
human2.fName = "Jane"
human2.lName = "Doe"
human2.age = 23
human2.gender = "Female"
print(human2.__str__())
```

Output:

```
First Name: Jane
Last Name: Doe
Age: 23
Gender: Female
```

There's a lot more to talk about but for the sake of brevity, I'll let you expirement with objects on your own time.

## 12.4 Inheritance

Inheritance is as the name implies, inheriting traits from a parent class. Continuing with our human class example, suppose a student inherited traits of a human while adding its own unique traits. This makes sense, as all students are humans but not all humans are students.

Here's the syntax for inheriting a class:

```python
class human():
    def __init__(self, fName, lName, age, gender):
        self.fName = fName
        self.lName = lName
        self.age = age
        self.gender = gender

    #__str__ returns a string in a legible manner to the user
    def __str__(self):
        return "First Name: " + self.fName + "\nLast Name: " + self.lName + "\nAge: " + str(self.age) + "\nGender: " + self.gender

class student(human):
    def __init__(self, fName, lName, age, gender, grade, classes, grades, gpa):
        super().__init__(fName, lName, age, gender)
        self.grade = grade
        self.classes = classes
        self.grades = grades
        self.gpa = gpa

    #this __str__ overrides human's original __str__() method
    def __str__(self):
        return "First Name: " + self.fName + "\nLast Name: " + self.lName + "\nAge: " + str(self.age) + "\nGender: " + self.gender + "\n:Grade: " + str(self.grade) + "\nClasses: " + str(self.classes) + "\nGrades: " + str(self.grades) + "\nGPA: " + str(self.gpa)

testHuman = human("John", "Doe", 21, "Male")
print(testHuman.__str__())
testStudent = student("John", "Doe", 21, "Male", 12, ["CSE30", "MATH19A", "WRIT2"], ["A", "B", "A"], 3.5)
print(testStudent.__str__())
```

Output:

```
First Name: John
Last Name: Doe
Age: 21
Gender: Male
First Name: John
Last Name: Doe
Age: 21
Gender: Male
:Grade: 12
Classes: ['CSE30', 'MATH19A', 'WRIT2']
Grades: ['A', 'B', 'A']
GPA: 3.5
```

## 12.5 Inheritance vs composition

I don't think you'll need to go over this in depth for your intro CS classes so I'll just give a really brief summary over this topic.

Inheritance allows you to pass and extend methods from a base class to child classes so you don't need to rewrite the same code for similar functionality. The problem with inheritance lies in the fact that it's not very flexible with it's passing. For our earlier human, student example, let's say we wanted to add another class to the student like tutor. Class tutor and class student have different properties and characterstics and we can't extend one while getting the same properties from another class without some wonky workarounds.

Here's where the idea of composition comes into play. Instead of inheriting everything from different classes, we should instead try to compose classes from a culmniation of functions and objects.

# 13. Recursion

Recursion is a very common programming term. Essentially, it is the process of defining and executing something in terms of itself. In other words, it's performing code blocks repeatedly inside itself or in other functions.

Here's an example to visualize recursion in python:

```python
def recursiveMultiplication(x, y):
    if (x*y < 1000):
        recursiveAddition(x*y, y)
    else:
        print(x*y)

recursiveMultiplication(5,2)
```

Output:

```
1280
```

In its first iteration, `x*y` equals 10. 10 is less than 1000 so we call the function again, this time passing in new numbers 10 and 2. 10\*2 = 20, which is again less than 1000. The process repeats and eventually we get 1280. Here's the chain:

| Iteration | x    | y   |
| --------- | ---- | --- |
| 1         | 5    | 2   |
| 2         | 10   | 2   |
| 3         | 20   | 2   |
| 4         | 40   | 2   |
| 5         | 80   | 2   |
| 6         | 160  | 2   |
| 7         | 320  | 2   |
| 8         | 640  | 2   |
| 9         | 1280 | 2   |

One common bug with recursion is the maximum recusion depth error. This happens when your program never stops recursively calling itself. Think of it as an infinite loop. The problem usually stems from there being no exit case.

Once the final recursive loop executes, the program begins to linerally unravel. From the above example, after iteration 9, iteration 8 can finally complete itself. In iteration 8, the if loop was executed but the code underneath it was never run (even though there is nothing there). Once iteration 9 is complete and the print statement is run without another recursive call, iteration 8 can complete itself as the line `recursiveAddition(x*y, y)` has finally finished executing.

# 14. Conclusion

This concludes the intro to python guide! If you read all the way through, you should be acquainted with the majority of topics you're intro CS courses will cover. Please keep in mind that while this guide is long, it was not designed to cover EVERY topic that comes up in your CS classes. In other words, pay attention still! Feel free to come back to this guide as a reference for syntax but also note that there are plenty of other online resouces out there.

CS is a really fun major and I'm sure you'll enjoy the process. Enjoy the content and good luck!
