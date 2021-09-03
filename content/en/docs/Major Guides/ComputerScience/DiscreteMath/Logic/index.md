---
title: "Logic"
linkTitle: "Logic"
weight: 1
icon:
draft: true
resources:
- src: "**gates_truth_tables*.jpg"
  params:
    byLine: "Diagram: Abels, Seth & Khisamutdinov, Emil. (2015). Nucleic Acid Computing and its Potential to Transform Silicon-Based Technology. DNA and RNA Nanotechnology. 2. 10.1515/rnan-2015-0003."
description: >
  Introduction to Logic.
---

# Logic
The knowledge you gain about logic from Discrete Math (CSE 16) and Computer Systems and Assembly Language (CSE 12) will be some of the most commonly used skills in your career because of how frequently we use conditional statements and try to simplify them in code.

## Implication

## Truth tables

## define proposition

## Logic Gates
This is one of the most common concepts you will come across when doing any programming. So, you will eventually memorize these, if you have not seen them before just from how often you will need to use them. All of the following gates are boolean/binary operations, which means that the inputs and outputs can only be True (1) or False (0) and nothing else and nothing in between.

### **AND**
The AND gate can take in any number of input greater than 1. The truth table for the AND gate and its appearance in digital logic design is shown below.

In short, the AND gate returns/outputs a True (1), *only* when *all* of its inputs are True (1). It returns/outputs a False (0) otherwise (i.e. when at least one input is False (0) ).

- Example: You want to check if A **AND** B **AND** C **AND** D are all True (1).

- Example: You are making a new social media and working on how to have a user create a new account. You need to check if the user entered a valid email **AND** they are over a certain age **AND** entered a secure password.

### **OR**
The OR gate can take in any number of input greater than 1. The truth table for the OR gate and its appearance in digital logic design is shown below.

In short, the OR gate returns/outputs a True (1), when *at least* one of its inputs are True (1). The other inputs can be anything else - there just has to be at least one True (1) in the inputs. It returns/outputs False (0) when all of the inputs are False (0).

- Example: You want to check if any one of A **OR** B **OR** C **OR** D are True (1).

- Example: You are making a scheduler. You want to check if the timer for the current task at hand has run out **OR** if the current task has finished so you can move on to another task. (This is one algorithm that a CPU may use schedule tasks in your computer!)

### **NOT**
The NOT gate (also called an inverter) can take in 1 input and invert it. The truth table for the NOT gate and its appearance in digital logic design is shown below.

In short, if the input is a True (1), then the output is a False (0). If the input is a False (0), then the output is a True (1).

- Example: You want to invert the truth value of one variable A.

- Example: You are making a game and want to check when the player in the game is alive or dead so you know to continue the game or display the "game over" message. You make a conditional statement to continue running the game while the player is **NOT** dead.


## logic laws handout

## rules of inference























