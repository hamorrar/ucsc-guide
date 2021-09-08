---
title: "Proofs"
linkTitle: "Proofs"
weight: 1
icon:
draft: false
- src: "**rules_of_inference*.png"
  params:
    byLine: "Diagram: skedsoft.com"
description: >
  Introduction to Proofs.
---

# Proofs
The proof building 

## Contradiction

## Contrapositive

## Induction

## Direct proofs

## **Rules of Inference**
This handout will be your best friend when doing some more formal boolean algebra proofs (see the Proofs section here). Like the previous handout, I will explain one rule from this one so you know how to read and use it when you have a formal proof to solve.

{{< imgproc logic_laws Fill "871x729" >}}
A reference chart for the rules of inference.
{{< /imgproc >}}

(Click <a href="rules_of_inference.png">here</a> to download the image if you want to save it for safe keeping.)

### Notation in the Rules of Inference
The $\lnot$ symbol is another way is representing a negation/inversion. The $\therefore$ symbol is called "therefore" and means therefore, you can think of it as an equal sign for now. It will make more sense in the example below. That is all the *new* notation in the handout! The rest should be explained in previous parts of the guide!

### Formal Logic Proof
Before we get to the example, you need to be familiar with what is and how to make a formal proof with the Rules of Inference. In general, these are made with two columns, left side has the boolean expressions that you are applying the Rules of Inference to and then the result and the right side as the name of the rule that you used to get to that result. A few rules and then the example to tie it all together:
1. Two columns: left has the actual boolean expressions, right has the name of the the rule you applied and the line numbers for the expressions involved.
1. Number each line starting from 1.

I know it is annoying to always "show your work", but it is easy to get lost or make a small mistake in the proof and then the answer is off or you cannot get to the correct answer. There are many ways to make a proof for a given problem, so these rules are in place to make it clear to the reader *how* you solved it and to yourself to follow your process to easily backtrack if something went wrong. Believe me, it is a time saver.

### Rules of Inference Example
I think the easiest way to understand how to use and read this chart is by making a small proof and walking you through my thought process! I will put the proof up first then explain it under.

Given: $(p \land q) \rightarrow r$, $p \rightarrow p$, $q$. Prove $r$.

 <table>
  <tr>
    <th>Expressions</th>
    <th>Reasoning</th>
  </tr>
  <tr>
    <td>1. $(p \land q) \rightarrow r$ </td>
    <td>Hypothesis 1</td>
  </tr>
  <tr>
    <td>2. $q \rightarrow p$ </td>
    <td>Hypothesis 2</td>
  </tr>
  <tr>
    <td>3. $q$ </td>
    <td>Hypothesis 3</td>
  </tr>
  <tr>
    <td>4. $p$ </td>
    <td>Modus Ponens, lines 2 and 3</td>
  </tr>
  <tr>
    <td>5. $p \land q$ </td>
    <td>Conjunction, lines 3 and 4</td>
  </tr>
  <tr>
    <td>6. $r$ </td>
    <td>Modus Ponens, lines 1 and 5</td>
  </tr>
</table> 

You are given three "hypotheses", which are the expressions that are given to you to use to solve for $r$. You are trying to derive $r$ from these three hypotheses. I like to list out the given hypotheses first, so they are there when I want to use them later, but you can write them down you need them as you go through the proof too.

Now to get to line 4, I look at the rules chart and I see what kind of rules I can apply to any previous lines and see if that gets me anything that can be useful. In this case, I see that Modus Ponens says if you have a line that says $p$ and a line that says $p \rightarrow q$, you can get $q$ as a result. I know the letters are a bit off but that is okay as long as you keep it consistent, you can make a substitution, so you can temporarily think of the $p$ in the proof as the $q$ in the chart and vice versa.

The logic behind Modus Ponens applied to line 4 is that if you have the value of $q$ in line 3 and you have the expression that says $q$ implies the value of $p$, then you can use $q$ you have to get the value of $p$. I think of this one as "unlocking". I need to get a $q$ because I have something that tells me that $q$ "unlocks" a new value that I need, which is $p$.

Put into a more concrete example, let's say $q =$ it is raining and $p =$ get an umbrella. Then you have a line that says $q \rightarrow p$ (i.e "if it is raining, then get an umbrella). You can observe that is raining, so we have established $q$ to be True (which is what line 3 represents in the proof). We have a statement (the implication arrow) that says what to do if it is raining, so we can conclude $p$ from that, which is to get an umbrella.

In line 5 of the proof, this is using the Conjunction rule, which allows you to combine any expressions in the proof so far with an AND ($\land$) between them. In this case, I see that it would helpful to do that because Hypothesis 1 on line says that if you have $p \land q$, you can get $r$, which is what we need.

Finally, I apply Modus Ponens again to lines 1 and 5 to get $r$ from $p \land q$ and $(p \land q) \rightarrow r$.

That's it! That was a walk through of the smallest proof I could find in my notebook! Congratulations on your first mathematical proof!

## examples using rules of implication and logic laws