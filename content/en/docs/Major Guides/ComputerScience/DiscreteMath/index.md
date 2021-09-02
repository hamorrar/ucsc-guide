---
title: "Discrete Math"
linkTitle: "Discrete Math"
weight: 1
icon:
draft: false
resources:
- src: "**subset*.png"
  params:
    byline: "Photo: OnlineMathLearning.com"
description: >
  Introduction to Logic, Set Theory, Proofs, and Counting.
---

# Set Theory
Set theory is the branch of mathematical logic that studies sets, which can be informally described as collections of objects. Although objects of any kind can be collected into a set, set theory, as a branch of mathematics, is mostly concerned with those that are relevant to mathematics as a whole. Founded by German mathematicians Richard Dedekind and Georg Cantor in the 1870s ([Wikipedia](https://en.wikipedia.org/wiki/Set_theory)).

## Definitions

**Set:** a collection of objects, where order and repetition does not matter. Sets can hold any type of objects, not strictly 1 character numbers or letters.

**Set Notation:** Sets are usually surrounded by curly braces with commas separating elements and when assigned to a variable, the convention is to use a single capital letter (although there may be exceptions).

**Element:** The objects inside a set.

**Element Notation:** When you want to note a specific element from a set, you use the $\in$ symbol. When an element is not in a set, you use the $\notin$ symbol.
  
  - Example: Written as $1 \in A$. Read/Spoken as "1 is an element of (set) A" OR "1 is a member of (set) A".
  - Example: Written as $34 \notin A$. Read/Spoken as "34 is not an element of (set) A" OR "34 is not a member of (set) A".

**Examples:** $A = \\{1, 2, 3, 4\\}$. $B = \\{a, b, c, d\\}$. $C = \\{cat, dog, cow, fox\\}$.

> Note: If you see "$\dots$" in a set that means that it should be clear what elements come next infinitely (i.e. this is the pattern for the set and it does not end).

---

## Common Sets
These are special sets that are used across mathematics and computer science theory (algorithms).

- $\mathbb{R}$ - called "real numbers". This set has any decimal number of any precision.
  - Examples: 1.0, 388.09384, 3.1415, -1005.6400009
- $\mathbb{N}$ = called "natural numbers". This set has the counting numbers that you use everyday. Depending on context, they may start with 0 or 1, so be careful.
  - Example: $\\{0, 1, 2, 3, 4, \dots\\}$
- $\mathbb{Z}$ - called "integers". This set has any positive or negative whole number.
  - Example: $\\{\dots, -3, -2, -1, 0, 1, 2, 3, \dots\\}$
- $\mathbb{Q}$ - called "rational numbers". This set has the result of dividing any two integers, but not 0 in the deminator.
  - Examples: $\frac{3}{2}, \frac{2}{4}, \frac{-24}{97}$
- $\emptyset$ OR $\\{\\}$ - called "empty set". This set has no elements in it.

---

## Cardinality

**Defintion:** The size/length of the set.

**Notation:** Vertical bars around the name of the set.

  - Example: $A = \\{1, 2, 3, 4\\}$. The cardinality of set A $= |A| = 4$.

Some sets are considered countable and some are considered uncountable. Simply, a set is countable if you can use the natural numbers to count the set in question. A set is uncountable if you cannout use the natural numbers to count it. There are also finite and infinite sets. A set is infinite is it has infinitely many elements and finite if it has a finite number of elements.

---

## Subsets

**Definition:** One set is a subset of another if all of the elements of one set can be found in the other.

**Notation:** $A \subset B$ OR $A \subseteq B$. The "$\subset$" symbol is called "proper subset" and the "$\subseteq$" is called "subset".

> Note: There is a little line under the symbol in the second example. This subtle difference between the two symbols is similar to $<$ and $\le$.

**Example of proper subset:** Let $A = \\{1, 2, 3, 4\\}$ and let $B = \\{1, 2, 3, 4, 5, 6, 7, 8\\}$. In this case, $A \subset B$ because all of the elements in set $A$ can be found in set $B$, but $B$ has some elements that $A$ does not. That is how it is written, but when it is read/spoken, you say "(set) $A$ is a proper subset of (set) $B$".

**Example of subset:** Let $A = \\{1, 2, 3, 4\\}$ and let $B = \\{1, 2, 3, 4\\}$. In this case, $A \subseteq B$ because all of the elements in set $A$ can be found in set $B$ and the two sets happen to be the same set. That is how it is written, but when it is read/spoken, you say "(set) $A$ is a subset of (set) $B$".

**Visually:** 
<!-- <div align="center" width="100" height="100"> -->
{{< imgproc subset Fill "400x450" >}}
A visual example of subsets and proper subsets
{{< /imgproc >}}
<!-- </div> -->

---




















