---
layout: posts
title: PyconDE report
categories: posts
---

<h2> {{ page.title }} </h2>

I attended PyconDE 2013 in Cologne, Germany. I also went last year in Leipzig.

<!-- more -->

I attended to 2 PyCons and so far, and I was never disappointed even though PyCon is one of the few conferences where, even as a speaker, 
you're going to have to buy a ticket, so you tend to expect the best.
The talks were overall good, with a few highlights mixed in (I'll get to that in a minute) but also a few lowlights
like a project manager straight out of a time machine explaining how he gets small teams to work "efficiently".

### devpi rocks
Holger Krekel introduced [devpi](http://doc.devpi.net/latest/) which is a next generation PyPI-compatible server.
The project is in a working state and full of awesome ideas like staging and propagation of packages and
index inheritance to restrict write access.
We have our own [PyPI caching server implementation](https://github.com/yadt/pypiproxy) which was needed to upload private
packages but we're totally dumping it for devpi.

### Python is slow
Many talks were about increasing the performance of python programs either by compiling to C, using some form of JIT or even
by offloading code to fast languages like LUA at runtime.
All of these approaches are quite elegant in my opinion as they do not really cost anything in readability (except for
the part where you embed LUA code, but LUA is also a very elegant low-level language if you do not need advanced features like
string operations).

### Continuous improvement
Compared to PyconDE 2012, the mean time of the talks increased (there were a lot of 20 minute talks in 2012, and that's
hell of a short timeframe to talk about something). There were mostly one hour or half-hour talks this year.

The catering was the worst I ever encountered at a conference though, so that's something to keep in mind.
There was either coffe or juice (no club mate!!!) but only downstairs in one out of two buildings, so just hanging around in the conference
area talking to people was not really an option.
And the attendees really were the highlight, because Pycon attracts everyone, from low level optimizers to scientists
and web developers.

### See you in Berlin!
I am looking forward to PyconDE 2014 which will be in Berlin.
