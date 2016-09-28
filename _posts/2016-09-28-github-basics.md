---
layout: post
title: Git Command Basics - Part 1
---

## What every new dev needs to know

College taught me a lot about software and how to build it. What it failed to teach me was what the software development life cycle looks like in the real world.

We never learned about agile, waterfall, testing, git, qa and many other integral parts of any software engineer's daily activities. Interestingly, these are some of my favorite parts about my job.
In future posts I'm going to get into some of the other topics, but here I'm going to focus on git.

This is going to be Part 1 of my Git Command Basics series, it's going to focus on all of the simple things, nothing too complicated. Just the basic commands that every new dev should have a basic understanding of.

I'm going to assume you know how git works at a high level. If you don't, check it out [here](https://www.atlassian.com/git/tutorials/what-is-git/). In my experience, most new devs
use a GUI, unfortunately a lot of GUIs don't translate well across machines, have bugs or struggle with their ability to properly handle merge conflicts. So I suggest using the terminal to handle your interactions
with git.

Then, at the end I'll post a link to my .gitconfig so you can see what aliases I use to make my life easier.

## Simple Commands

Lets assume our current repository only has 2 files

- file1.txt
- file2.txt

Lets say that we've made changes to both files, but we only want to commit file1.txt

```
git add file1.txt
```

This stages the file to be committed. (Usually I only stage things right before I'm ready to commit) This will not stage file2.txt, it will still remain as an unstaged file.

```
git commit -m "This is going to commit the staged files, file1.txt in this case"
```

This will commit file1.txt to the local copy of our repository. file2.txt is still marked as unstaged, and we have a new commit in our history. To see this history
we can use the following command

```
git log
```

This will show all of the commits in the commit history. The top one will be adding file1.txt with the commit of "This is going to commit the staged files, file1.txt in this case"
Then when we are ready we can push the commit up to the remote repository with:

```
git push
```

It's that easy, we just added a file to be tracked, commit the changes and then pushed them up to the remote repository. In Part 2, I'll dive into rebasing!

## Git Config

Here's a link to my [.gitconfig](https://github.com/MattJGlick/dotfiles/blob/master/gitconfig)

Here is a snapshot of some of my favorite aliases:

```
[alias]
    br = branch                         
    cm = commit -m 
    co = checkout
    cob = checkout -b               # created a new branch
    st = status
    rbi = rebase -i                 # rebase based on a branch
    rbc = rebase --continue         # continue a rebase
    pf = push --force-with-lease    # overwrite the branch on the remote repo
```
