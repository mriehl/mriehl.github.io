---
layout: posts
title: Less keywords is more
categories: posts
---

<h2> {{ page.title }} </h2>

The go language is pretty cool. Coming back from a lot of python, it's admittedly difficult to go back to compiling and static typing, sure. But it feels so much safer to know that your program can't suddenly explode because some 3rd-party lib decided to return an int instead of a dictionnary.

<!-- more -->

There's no `while` in go. Instead of `while`, you use `for`. Makes sense and we get rid of a keyword. Cool!

Another great thing is the if-with-initializer-statement. You can add a declaration statement to an if condition, e.G.

<pre><code>
if isNeitherFizzNorBuzz := (len(accu) == 0); isNeitherFizzNorBuzz {
        accu += strconv.Itoa(number)
    }
</code></pre>

as opposed to e.G. python, where you'd use two statements instead :

<pre><code>
is_neither_fizz_nor_buzz = not accu
if isNeitherFizzNorBuzz:
    accu = str(number)
</code></pre>

The go version is totally readable because essentially to understand the if, you just need to read the first two words.
`if isNeitherFizzNorBuzz`, that's exactly what that thing does. This I like! You can extract the if condition in a variable without having to actually do it on a separate line. And it's still readable.

Going a bit further, the `if` keyword has actually two uses, not unlike the `for` is used both for `for`-loops and for `while`-loops.

* Branches. That's straightforward, we all expect that from if.
* Error handling. Yeah, that's right. The go way of error-handling a called function is

<pre><code>
if err:= Function(); err!=nil{
    // TODO deal with error
}
</code></pre>

That now requires to read 3 words but once again it's straight to the point.
"If err Function", that's exactly what it does. If the function errors, then do that.
