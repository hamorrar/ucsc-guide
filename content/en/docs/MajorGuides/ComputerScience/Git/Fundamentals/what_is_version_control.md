---
date: 2021-09-15
title: "What Is Version Control?"
linkTitle: "What Is Version Control?"
description: "An explanation of version control and how it pertains to Git."
weight: 1
author: Steven Mak
---

Before delving into the specifics of Git, we must first explain what version control is because Git is a version control system. This article will explain what version control is and what're its benefits.
 
## Definition

Anything from text documents to software go through cycles of development and revisions to get to the current place that they're at. Much of the time, multiple people are modifying different things at once or even making conflicting changes, resulting in a non-linear series of changes. 

How all these issues are dealt with depends on the version control system being used. In essence, anything that allows people to manage changes done to something is a version control system. There are many applications of version control in our daily lives outside of programming. One example of this is being able to check version history and revert changes in Google Docs.

<div class="card rounded p-2 td-post-card mb-4 mt-4" style="max-width: 294px">
	<img class="card-img-top" src="../version_control_example.jpg" width="294" height="497">
	<div class="card-body px-0 pt-2 pb-0">
		<p class="card-text">
		How Google Docs implements version control
		<small class="text-muted"><br>Photo: docs.google.com</small>
		</p>
	</div>
</div>

We will dive into how Git implements version control in the next article, but for now, we'll talk about its benefits when it comes to developing software.

​

---
## Benefits for developing software

Significant pieces of software are virtually never developed completely alone and undergo countless changes. This results in a potentially complicated net of changes which must be kept track of to do things like revert a specific set of changes or keep track of who did what. It is because of this that version control is vital for software development. 

<div class="card rounded p-2 td-post-card mb-4 mt-4" style="max-width: 500px">
	<img class="card-img-top" src="../branch-graph-example.png" width="835" height="622">
	<div class="card-body px-0 pt-2 pb-0">
		<p class="card-text">
		A graph of changes to a project over time.
		<small class="text-muted"><br>Graph: Made using the Git Graph Visual Studio Code extension</small>
		</p>
	</div>
</div>

Whatever field of computer science you end up doing, you will always encounter the usage of version control in some way or another, which is why lower division computer science courses such as CSE 12/L and CSE 13 make you get into the habit of using Git. Although the projects you do in those courses will be alone and not with other contributors, it is still extremely useful for reverting bad changes, seeing what was done when, and for other reasons that will be explained in the next article.

​

---

​

Now that we've covered what version control is, the next article will explain what Git does to implement a version control system to reap the benefits of using it as explained above. 