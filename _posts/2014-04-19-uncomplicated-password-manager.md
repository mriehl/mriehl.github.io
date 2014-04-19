---
layout: posts
title: Uncomplicated password manager
categories: posts
---

## {{ page.title }}
Password managers have become a big deal with all the recent events (heartbleed, NSA, ...). Most people seem to be using BLOB-based password managers nowadays (truecrypt, keepass, 1password, ...) but I think they suck.

<!-- more -->

### My gripe with most password managers
They require me to carry a blob around or (even worse) upload it to a storage service (e.G. dropbox). They're not usable from the command line. And they're (mostly) awkward on a mobile device.

### Enter the vault

I'm using [vault](https://github.com/jcoglan/vault) with a few additions.
The basic idea is that passwords are computed from a secret (your master key) and an arbitrary service name.

For example, to access my GitHub password, I use the service name "github" and my master key.

Using my own hosted [vault site](http://max.riehl.io/vault/), built by @jcoglan, I can obtain my passwords from everywhere, provided I have a connection. This is fully done in client-side javascript, so I don't need or rely on HTTPS. The code is open source and small, so I can audit it myself.

### Small improvements
Vault itself is already pretty awesome. It works everywhere provided I have a browser with javascript. Soon, even my fridge will be able to get my passwords, I think. But when working on a linux machine, it could better. I don't really want to switch to a browser for a git push, for example.

I thus wrote two little scripts:

{% highlight bash %}
#!/bin/bash

function require(){
    PROGRAM="$1"
    command -v $PROGRAM >/dev/null 2>&1 || {
        echo "Missing required program: $PROGRAM"
        exit 1
    }
}

require vault
require xsel

SERVICE=${1:? "Usage: $0 SERVICE_NAME"}

vault -p $SERVICE | xsel -b
{% endhighlight %}

This one (I call it [`passme`](https://github.com/mriehl/dotfiles/blob/master/bin/passme)) uses the nodejs vault program from @jcoglan to generate a service password (prompting interactively for the master key) and pipes it into `xsel -b` (which puts it in the clipboard). This does not leave any trace on the machine (except for the service name), so I don't care about prying eyes.

After having used my password, I have another script, [`byepass`](https://github.com/mriehl/dotfiles/blob/master/bin/byepass)

{% highlight bash %}
#!/bin/bash

function require(){
    PROGRAM="$1"
    command -v $PROGRAM >/dev/null 2>&1 || {
        echo "Missing required program: $PROGRAM"
        exit 1
    }
}

require xsel

echo -n "Your password is in another castle" | xsel -b
{% endhighlight %}

which basically just clears my password from the clipboard.

### Final result

I have an extremely simple flow when working on the command line.

<script type="text/javascript" src="https://asciinema.org/a/9017.js" id="asciicast-9017" async></script>
