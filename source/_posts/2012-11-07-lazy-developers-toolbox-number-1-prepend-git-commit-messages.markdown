---
layout: post
title: "Lazy Developer's Toolbox #1 - Prepend git commit messages"
date: 2012-11-07 17:21
comments: true
categories: lazy toolbox git
---

Being a good citizen of the open source community means following the rules concerning software development defined by the team. One of it, [sadly the one very frequently neglected](http://www.commitlogsfromlastnight.com/), is meaningful commit message with a reference to the task you worked on. Such an info can be later leveraged by tools like FishEye, but that's another story. So what's the problem with that for lazy guys like me?

<!-- More -->

On my open source nigth shifts I'm mainly involved in [Arquillian project](http://arquillian.org) (more about it soon). All our code is [on GitHub](http://github.com/arquillian). Each time I work on some task I'm creating a feature branch with the corresponding name (for instance [ARQ-1186](https://issues.jboss.org/browse/ARQ-1186)). When I'm done with the work (or consistent part of it) I commit my changes:

	$ git commit -m"[ARQ-1186] Introduced new property in configuration  \
	file to define default (global) transaction mode"

But there's a little annoying problem with this... I'm not really that keen to memorize the issue number and type these few extra characters by hand each and every time (yes! I'm that lazy!). Obviously you can always customize your shell by using [git-completion](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash) for instance, but that only solves part of the problem. You don't need to remember this bloody issue number, but you still need to type it.

So one day I was wondering if it would be possible to prepend commit message using branch information. It turned out to be damn easy.

### Git hooks

Git is very powerful tool so no suprise that it has a concept of [hooks](http://git-scm.com/book/en/Customizing-Git-Git-Hooks). Hooks are scripts written in any language your shell supports executed at the given point of the git workflow. In our case we are interested in executing script on client side before we commit. Let's have a look what kind of local hooks we have in our repository folder `.git/hooks`:

	├── applypatch-msg.sample
	├── commit-msg.sample
	├── post-update.sample
	├── pre-applypatch.sample
	├── pre-commit.sample
	├── prepare-commit-msg.sample
	├── pre-rebase.sample
	└── update.sample

The names are rather self explanatory - we should use `prepare-commit-message` hook to achieve our goal. 

### A little bit of bash fu

In order to increase our productivity (or keep our lazy nature happy) we simply rename `prepare-commit-msg.sample` to `prepare-commit-msg`, paste the script listed below and ensure that the file is executable.

{% gist 1396344 prepare-commit-msg.sh %}

From now on we don't need to remember the issue number anymore! Executing 
	$ git commit -m"Introduced new property in configuration file \ 
	to define default (global) transaction mode" 
will result with `[ARQ-1168] Introduced new property in configuration file to define default (global) transaction mode` as commit message. Life is so easier now ;)

_**Note:** If you are using Eclipse git integration this approach won't work. EGit is not aware of commit hooks._
