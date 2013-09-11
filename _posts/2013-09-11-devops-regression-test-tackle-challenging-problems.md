---
layout: posts
title: DevOps regression test
categories: posts
---

# DevOps regression test: tackle challenging problems

An easy way to determine if DevOps is working for you is tackling challenging
problems. So challenging, in fact, that it would be impossible to succeed unless
everyone works together. Also everyone should have a stake in this (if they do not,
you've already failed the test).


A daring gambit you say? I also thought so. But not so much.
<!-- more -->
## Full throttle
Our company decided to do such a thing. Ambitious goal (moving a lot of VMs around),
little time, and all this is in an environment with a lot of change.

The steps involved in a VM migration require understanding both the OPS and DEV POVs.

In order for this to work, we currently have a 3-day camp going on where basically the whole IT (150+ people)
is dedicated to making progress on the migration.


## Preparations and aces up the sleeve

The stage is set up nicely (having at least one scrum master in the driving force seems to help a lot).
Solid documentation was made available, and basically anyone can do everything (him|her)self.
This is because we run a [self-service virtualization](https://github.com/ImmobilienScout24/lab-manager-light) coupled with a [package-based deployment](http://www.yadt-project.org) which just radiates simplicity.
Whatever you want to do boils down to modifying a file and continuous integration / continuous delivery ensures that
your changes are tested and deployed without requiring you to even lift a finger.

New DNS configuration? Edit a file.

VM needs a bigger hard drive? Edit a file.

Host has a new FQDN? Edit a file.

## Some random thoughts so far
 * It feels awesome working with so many people and just bashing through the issues
 * Coworking and pairing is at an all-time high
 * We are making good progress on all fronts
 * Knowledge is spreading extremely fast
 * Having clear responsibilities and *problem solvers* running around helps a lot, as well as good documentation
 * SVN = lots of contention. I think I was spoiled by git.

Also, I would not have expected intrinsic motivation to kick in so quickly.
I honestly can't wait to get back to work.
