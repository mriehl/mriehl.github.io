---
layout: posts
title: Improve your git commit messages today!
categories: posts
---

<h2> {{ page.title }} </h2>

I finally caught up with the git commit message best practice.
Linus' rants about GitHub commit / pull request quality ([example](https://github.com/torvalds/linux/pull/17)) helped a lot.
He's harsh but right - look at the kernel commit messages with `git log`. It's awesome.



I also found [an older post from tpope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) (catching up, like I said) that deals with best practice for commit messages.

If you're like me, you use vim to write commit messages and there is a quick win to write better messages starting today!
Just add
```
+au FileType gitcommit set tw=72
```
to your `.vimrc` and you're set! This will wrap lines at 72 characters when writing files of type `gitcommit`.
