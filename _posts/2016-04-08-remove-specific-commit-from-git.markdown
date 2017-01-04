---
layout: post
title:  "Removing a specific commit from Git"
date:   2016-04-08
categories: blog
comments: true
---

Today was one of those days that the team realises that one of the commits, from the past couple of days, was introducing all sorts of side effects. The commit itself was doing some heavy refactoring on a piece of code that wasn’t supported by unit tests, therefore introducing defects. The obvious thing to take from that is that you should ALWAYS have unit tests around your code. If you don’t this is your chance to write them before you refactor. But that’s a story for another day.

To solve the problem we decided to remove the buggy commit from our repository and redo the changes to the un-refactored code. This can be either a painless process (thanks git) or pretty painful. There are 4 ways to do so.

## The Clean way
This should be the first thing to try. In git version 1.7.2-rc2 onwards a new feature was introduced: **git revert --strategy resolve <commit>**. What this does for you it tries to revert your commit in a safe and fast way, by trying to carefully detect criss-cross merge ambiguities. The **--strategy** flag works the same way for git merge too. There more strategies to look for [here](https://git-scm.com/docs/git-merge#_merge_strategies).

## The hammer way
If the buggy commit is the last one in the repository then you can do: **git reset --soft "HEAD^"** and that will remove the last commit altogether

## The rebase way
The last, more versatile, option you have is using git rebase. Rebase can do all sorts of stuff for you like:

* Go back x revisions: **git rebase -i HEAD~x** (x=1,2,3,...). If you made a mistake while rebasing you can do: **git rebase --abort**
* Remove a specific commit using its id: **git rebase --onto commit-id^ commit-id**

Please note that all these changes are done locally. After completing everything you need to do git push.

### More Resources

* [https://www.git-tower.com/learn/git/ebook/en/command-line/advanced-topics/undoing-things](https://www.git-tower.com/learn/git/ebook/en/command-line/advanced-topics/undoing-things)
* [https://www.atlassian.com/git/tutorials/undoing-changes/](https://www.atlassian.com/git/tutorials/undoing-changes/)
* [https://sethrobertson.github.io/GitFixUm/fixup.html](https://sethrobertson.github.io/GitFixUm/fixup.html)
