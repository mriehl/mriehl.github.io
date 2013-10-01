---
layout: posts
title: An obscure python loop feature
categories: posts
---
<h1>{{ page.title }}</h1>
I just stumbled over one of python's dirty little secrets while going through the PySNMP examples.
SNMP is a very cool protocol because it's blazing fast, but boy is it ugly to use. PySNMP stays
true by also exposing a difficult to use API. Say hello to
{% highlight python %}
from pysnmp.entity.rfc3413.oneliner import cmdgen
{% endhighlight %}
<br/>
<!-- more -->
This somehow reminds me of the [guidelines on how to write unmaintaineable code](http://mindprod.com/jgloss/unmaindocumentation.html) (laughter guaranteed).
One of the examples featured a for loop followed up by an else clause:
{% highlight python %}
for oid, val in varBindRow:
            if not val.isSameTypeWith(rfc1905.endOfMibView):
                break
else:
    reactor.stop()
    return
{% endhighlight %}

I first thought it was an indentation bug in the code, but it is actually [valid python](http://docs.python.org/release/1.5/tut/node23.html):
> Loop statements may have an else clause; it is executed when the loop terminates through exhaustion of the list (with for) or when the condition becomes false (with while), but not when the loop is terminated by a break statement. This is exemplified by the following loop, which searches for prime numbers:
{% highlight python %}
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
           print n, 'equals', x, '*', n/x
           break
    else:
         print n, 'is a prime number'
{% endhighlight %}
You can avoid using state variables with it but I think it costs too much readability
in algorithms where you should be extracting functions as much as possible.<br/>
In this case the code fails to reveal what x means. IMHO it would be better to
make explicit that you are searching for the first nontrivial divisor, and a
number is prime when it has no nontrivial divisors. This allows you to extract a function
```first_nontrivial_divisor(number)``` and replace dubious break-based
flow control with a return statement.
