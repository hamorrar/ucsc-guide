---
title: "Python Guide Pt.2"
linkTitle: "Python Guide Pt.2"
author: "James Zhou"
date: "2021-09-22"
weight: 1
icon:
draft: false
description: >
  Part 3 of a comprehensive guide covering an introduction to python curtailed towards the curriculum of CSE20 and CSE30. This part will cover the advanced topics covered in CSE20 and 30.
---

# Python Guide Part 3

## Table of Contents

- [Python Guide Part 3](#python-guide-part-3)
  - [Table of Contents](#table-of-contents)
- [1. Generators](#1-generators)
- [2. Dictionaries cont.](#2-dictionaries-cont)
- [3. Classes and objects](#3-classes-and-objects)
  - [3.1 Classes](#31-classes)
  - [3.2 Objects](#32-objects)
  - [3.3 More complex classes](#33-more-complex-classes)
  - [3.4 Inheritance](#34-inheritance)
  - [3.5 Inheritance vs composition](#35-inheritance-vs-composition)
- [4. Recursion](#4-recursion)
- [5. Conclusion](#5-conclusion)

# 1. Generators

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

# 2. Dictionaries cont.

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

# 3. Classes and objects

Python is an object-oriented programming language, meaning that everything inside of python is an object (besides control flow). This chapter will cover what objects are and the classes that define different objects.

## 3.1 Classes

Classes in python serve as object blueprints. They detail what an object consists of --- its characteristics if you will. Similar to how we classify certain animals under specific classes (domains), we can do the same with objects. Let's look at the basic syntax of creating our own python class:

```python
class human:
    name = "Joe"
    age = 0
    gender = "Male"
```

This is our very own human class. Let's next look over how to make an object of class human.

## 3.2 Objects

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

## 3.3 More complex classes

To make dynamic objects, we need to have flexibility with our class constructors. Here's how to add parameters, or constructors, to a python class using the function `__init()__`:

```python
class human():
    def __init__(self, fName, lName, age, gender):
        self.fName = fName
        self.lName = lName
        self.age = age
        self.gender = gender
```

Now, when we create a new human object, we can add some uniqueness to it. Using the `__init__()` function allows us to initialize an object using set parameters that the user can input. We always include self as the first parameter because we need to address the object itself when first initializing the arguments we pass to the constructor. We can add more functions using `def` but I'll let you experiment with that yourself.

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

There's a lot more to talk about but for the sake of brevity, I'll let you experiment with objects on your own time.

## 3.4 Inheritance

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

## 3.5 Inheritance vs composition

I don't think you'll need to go over this in-depth for your intro CS classes, so I'll provide a brief summary of this topic.

Inheritance allows you to pass and extend methods from a base class to child classes. This means you don't need to rewrite the same code for similar functionality. The problem with inheritance lies in the fact that it's not very flexible with its passing. For our earlier human, student example, let's say we wanted to add another class to the student, say "tutor". Class tutor and class student have different properties and characteristics, and we can't extend one while getting the same properties from another class without some wonky workarounds.

Here's where the idea of composition comes into play. Instead of inheriting everything from different classes, we should alternatively try to compose classes from a culmination of functions and objects.

# 4. Recursion

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

One common bug with recursion is the maximum recursion depth error. This happens when your program never stops recursively calling itself. Think of it as an infinite loop. The problem usually stems from there being no exit case.

Once the final recursive loop executes, the program begins to literally unravel. From the above example, after iteration 9, iteration 8 can finally complete itself. In iteration 8, the if loop was executed but the code underneath it was never run (even though there is nothing there). Once iteration 9 is complete and the print statement is run without another recursive call, iteration 8 can complete itself as the line `recursiveAddition(x*y, y)` has finally finished executing.

# 5. Conclusion

This concludes the intro to python guide! If you read all the way through, you should be acquainted with the majority of topics you're intro CS courses will cover. Please keep in mind that while this guide is long, it was not designed to cover EVERY topic that comes up in your CS classes. In other words, pay attention still! Feel free to come back to this guide as a reference for syntax but also note that there are plenty of other online resources out there.

CS is a really fun major and I'm sure you'll enjoy the process. Enjoy the content and good luck!
