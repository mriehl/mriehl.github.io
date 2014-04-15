---
layout: posts
title: (un)Security through transparency
categories: posts
---
## {{ page.title }}
There's always much talk about systems which are insecure by default. The
usual point being made is that a not-so-tech-savvy or uninformed user
will be running an insecure setup without ever noticing.
But what of the (supposedly) tech savvy people that offer their skills as a service?
<!-- more -->
### Incompetence as a service
Hosting services are definitely not known for staying on the bleeding edge of software.
In fact, they're not known for staying up to date either.
But running a PHP version from 2009 while also proudly delivering a
<pre><code>
x-powered-by $php-version-from-2009
</code></pre>

header to every get request is something new entirely.
It gets even better, when you call the helpdesk and complain about it they


* Don't understand what a header is
* Don't understand why it is problematic to expose this header
* Refuse to change anything because they cannot fathom _how it will affect their service_


### Rolling your own
As a conclusion,

 * don't use PHP
 * don't host a dynamic site where you have no control over it (unless you have proof that the provider is great)
 * in fact don't run a dynamic site unless you really need it
 * last but not least, do not insert easter eggs in your software if they can have an impact on security (I am looking at you PHP)!

   Why would you EVER want to expose your software version on a production system?!
