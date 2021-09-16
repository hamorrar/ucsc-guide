---
date: 2021-09-15
title: "How Git Works"
linkTitle: "How Git Works"
description: "An explanation on what exactly Git is."
weight: 2
author: Steven Mak
---

In the last article, we talked about what version control was. Now, we're going to cover how Git implements it. 

Note: As stated in [Fundamentals](../), it's okay if you don't understand the stuff covered in here immediately. Read through the article then go to [Basics](../../basics/), rereading this article as necessary.

## Fundamentals of Git

Git is a version control system which allows you to log changes made, reasons behind them, push these changes to replicate it in an external place, pull in changes from that external place to other places like another device, and more.

## Repositories (Repos)

A repository, or repo, is a collection files and directories (folders) in which changes can be made. Most Git repos are used for storing a unit of software, like a program. Repos stored in different places are called different things. A local repo is one that is on your own computer/device while a remote repo is one that is on an external server. These external servers can be hosted by various places. For example, UCSC hosts a GitLab server, which implements Git. However, they can also be places like GitHub or GitLab's own servers rather than something self-hosted like the school's servers on. 

<div class="card rounded p-2 td-post-card mb-4 mt-4" style="max-width: 500px">
	<img class="card-img-top" src="../git-bash-console.png" width="581" height="476">
	<div class="card-body px-0 pt-2 pb-0">
		<p class="card-text">
		An example of how to interact with a local repository.
		<small class="text-muted"><br>Photo: Git Bash Windows console</small>
		</p>
	</div>
</div>

<div class="card rounded p-2 td-post-card mb-4 mt-4" style="max-width: 1625px">
	<img class="card-img-top" src="../burdbot-repo.png" width="1625" height="631">
	<div class="card-body px-0 pt-2 pb-0">
		<p class="card-text">
		An example of a remote repository on Github.
		<small class="text-muted"><br>Photo: github.com</small>
		</p>
	</div>
</div>

### Creating repositories

We won't get into exactly how to do anything until [Basic Git Operations](../../basics/basic_git_operations), but we'll describe the the process for now. There are two main ways to create a local repo. The first is to clone it from an existing repo, usually a remote one. The other is to initialize it using the command line. How to create a remote repo depends on where the repo is stored. When it comes to a repo for classes, they will generally be pre-made on the school's GitLab server and shared with you. However, you can also create repos by navigating to the website and using it to create one, which is also the same way to create a remote repo on sites like [GitHub](https://github.com) and [GitLab](https://gitlab.com/users/sign_in).

## Making changes to repositories

As stated earlier, version control provides a way to track changes made. The way Git implements this is through something called commits, commit history, and branches. Commits made on local repos can be pushed to remote repos so that they're replicated. We'll explain this in further detail in [Basic Git Operations](../../basics/basic_git_operations), but this system of being able to make local repositories by cloning remote repositories and pushing changes to transfer them to a remote repo creates redundancies so that your changes persist even if your device's HDD or SSD fail. 

### Commits

Commits are a unit of changes to a file or batch of files labelled with a title and description. In Git, every  individual commit stores changes made from the previous commit, building on top of them instead of storing the entire repo's state. We will go over how to create them in [Basic Git Operations](../../basics/basic_git_operations).

### Commit History

As the name suggests, commit history is made up of past commits. Because each commit builds off of the last one, the visible commit history must be linear within a given branch (explained below) so it leads from the original state to the current state. 

<div class="card rounded p-2 td-post-card mb-4 mt-4" style="max-width: 600px">
	<img class="card-img-top" src="../burdbot-repo-commit-log.png" width="786" height="976">
	<div class="card-body px-0 pt-2 pb-0">
		<p class="card-text">
		An example of the commit history of a repo.
		<small class="text-muted"><br>Photo: Git Bash Windows console</small>
		</p>
	</div>
</div>

### Branches

By default, all repos created have one branch, the main or master branch. A branch consists of a series of commits and new ones can be created by branching off from another branch. There are many operations that can be done with branches, but we won't be getting into them because they're not needed for the lower division courses. 

## Getting Git on a local computer

To actually use Git on your computer, you first need to get it. If you're in or going into CSE 12/L, you'll need to use Git for Windows. If you're in or going into CSE 13, you'll be using Ubuntu. Ubuntu and MacOS in most cases should both come with Git by default. However, if you're on Windows, this isn't the case. If the ``Git`` command isn't available via the command line, download it from [here](https://git-scm.com/downloads).

## Making an account for remote repositories

Now that we've covered what repos and commits are, it's time to do some set-up prior to actually using Git. 

To make an account for school-related remote repos which you'll use in many computer science classes, go to the [school's self-hosted GitLab site](https://git.ucsc.edu). When creating a school account, do not use another site like GitLab directly or GitHub. Use your school email for the email, Cruz ID for your username, and make a password to register. 

If you want to create an account on a site hosting remote repositories to put personal projects in to using Git, use a site like [GitHub](https://github.com) or [GitLab](https://gitlab.com/users/sign_in).

--

Once you create an account, go to the next article, which will explain how to set up an SSH key for Git so that you can push and pull changes to/from the remote repository without having to authenticate using your password. 

Note: There are a lot more features Git has to provide apart from the ones listed in this article. As mentioned in [Git](../../), the primary purpose of these articles is have enough knowledge about Git to get through the lower division courses.