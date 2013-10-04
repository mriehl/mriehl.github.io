---
layout: posts
title: Fast and powerful integration testing with shtub
categories: posts
---

# Fast and powerful integration testing with shtub

YADT is a tool that orchestrates deployments and servers using the SSH
protocol, and while we use the Twisted framework which has a nice SSH implementation,
we're using subprocess calls to run the linux openssh program.

One a sidenote twisted conch is really interesting, but hostbased authentication is difficult
and [it seems to be impossible to get extended data from the client](http://stackoverflow.com/questions/7937651/receiving-extended-data-with-ssh-using-twisted-conch-as-client)
while the openssh client magically does all this and more.

An interesting part of using subprocesses for SSH is integration testing - how can you even mock such a thing?
The requirements of such an integration test would be

 * defining some stubs declaratively
 * calling your application
 * and finally asserting that certain things were called in some order.

But especially calling your application in a new process and have it use the stubs is totally nontrivial.

There is [MockProc](https://pypi.python.org/pypi/MockProc/) for very simple use cases but we're firing many
SSH calls and need fine-grained behaviour, so it won't do the job. Also, it's not thread safe :(

Enter [shtub](https://github.com/yadt/shtub), the shell command stub framework! Like MockProc, shtub exploits the fact that things
that come first in
your PATH can shadow things that come afterwards, and is thus able to replace any shell command you call
by a stub that is fully under your control.

MockProc's issues with parallelization are due to the need to manipulate your own environment,
but provided you can launch your application in a process, you do not need to manipulate the environment of the current process -
you just give the new process a patched one instead.

The great thing about shtub is that since it generates a file to replace the command, it is completely discrete
to whatever directory you happen to be in. It also uses JSON serialization to remember the stubs' state between calls.
In other words, you can parallelize the sh** out of it!

We just did and went from about ~5 minutes of integration testing to ~20 seconds while maintaining full correctness.
As a side effect, pybuilder [is now able to run integration tests in parallel](http://pybuilder.github.io/releasenotes/#version_0911).
