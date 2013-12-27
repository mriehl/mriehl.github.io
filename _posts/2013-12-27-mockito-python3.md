---
layout: posts
title: Mockito and python3
categories: posts
---

<h2> {{ page.title }} </h2>

In case you use mockito, you have probably noticed that it won't install on python 3 anymore.
<!-- more -->
Let's check it out in a vagrant box.
```bash
vagrant ssh
Last login: Fri Dec 27 11:00:09 2013 from 10.0.2.2

[vagrant@localhost ~]$ sudo pacman -Sy
:: Synchronizing package databases...
[vagrant@localhost ~]$ sudo pacman -S python-pip
resolving dependencies...
looking for inter-conflicts...

Packages (3): python-3.3.3-1  python-setuptools-2.0.1-1  python-pip-1.4.1-2

Total Download Size:    12.55 MiB
Total Installed Size:   87.56 MiB

:: Proceed with installation? [Y/n] 
:: Retrieving packages ...

[vagrant@localhost ~]$ sudo pip install mockito
Downloading/unpacking mockito
  Downloading mockito-0.5.2.tar.gz
  Running setup.py egg_info for package mockito
    Downloading http://pypi.python.org/packages/source/d/distribute/distribute-0.6.10.tar.gz
[...]
    error: invalid command 'bdist_egg'
    /tmp/pip_build_root/mockito/distribute-0.6.10-py3.3.egg
    Traceback (most recent call last):
      File "./distribute_setup.py", line 143, in use_setuptools
        raise ImportError
    ImportError
[...]
OSError: Could not build the egg.

----------------------------------------
Cleaning up...
Command python setup.py egg_info failed with error code 1 in /tmp/pip_build_root/mockito
Storing complete log in /root/.pip/pip.log
```

Obviously it is pulling distribute 0.6.10. Doesn't sound very bleeding edge (current distribute is 0.7.3 and that is just a wrapper since setuptools and distribute have been merged).

Why is it pulling that version specifically?

```bash
[vagrant@localhost ~]$ wget https://pypi.python.org/packages/source/m/mockito/mockito-0.5.2.tar.gz

[vagrant@localhost ~]$ tar xzvf mockito-0.5.2.tar.gz
[...]
[vagrant@localhost ~]$ cd mockito-0.5.2
[vagrant@localhost mockito-0.5.2]$ grep -Hirn "0.6.10" *
distribute_setup.py:49:DEFAULT_VERSION = "0.6.10"
[vagrant@localhost mockito-0.5.2]$ grep use_setuptools setup.py 
from distribute_setup import use_setuptools
use_setuptools()
```
Basically `distribute_setup` is a bootstrapping script for distribute that will download distribute. If you don't provide a `version` kwarg to `use_setuptools` then it will download the default which is a hardcoded "0.6.10".

### What you can do
Replace your `mockito` dependency with [`mockito-without-hardcoded-distribute-version`](https://github.com/mriehl/mockito-without-hardcoded-distribute-version). You don't need to touch your imports.
I basically just changed the name and removed the `distribute_setup` stuff.

Also, comment on [the pull request](https://bitbucket.org/szczepiq/mockito-python/pull-request/2/dont-download-distribute/diff) so that it gets merged.
