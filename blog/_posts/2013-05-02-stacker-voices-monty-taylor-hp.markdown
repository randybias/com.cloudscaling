---
author: Randy Bias
comments: true
date: 2013-05-02 17:00:00+00:00
layout: post
slug: stacker-voices-monty-taylor-hp
title: Stacker Voices&#58; Monty Taylor, HP
---

We talked with Monty Taylor of HP at the OpenStack Summit in Portland. Monty is the automation and deployment lead for cloud at HP. He’s also a member of both the OpenStack Technical Committee and the OpenStack Foundation Board of Directors.

// Check out [Monty’s feature profile] by [Cade Metz] in Wired Enterprise yesterday. //

  [Monty’s feature profile]: http://www.wired.com/wiredenterprise/2013/04/new-hackers-taylor/
  [Cade Metz]: http://twitter.com/cademetz

Monty leads the CI (continuous integration) project for OpenStack. In that role, he and his group have built testing systems that have made it possible for the OpenStack project to scale from a few dozen contributors for the Bexar release to more than 700 developers now pushing patches *daily* to the project.

Watch the video to learn more about:

  - OpenStack’s integrated code review system and gated commits
  - running the CI system as a single app across two public clouds, with resources donated by HP, Rackspace and eNovance
  - merging about 150 patches each day into the code base, and the 500+ that don’t make it
  - how gated commits interact with the CI system
  - using Google’s [Gerrit code review] system that feeds into Zuul for gating, which is connected to a [Jenkins server] with [Gearman worker support] for scaling
  - running tests in parallel with optimistic [pipelining] to save time

  [Gerrit code review]: https://code.google.com/p/gerrit/
  [Jenkins server]: http://jenkins-ci.org/
  [Gearman worker support]: http://gearman.org/
  [pipelining]: http://en.wikipedia.org/wiki/Pipeline_(computing)
  
Check out the video, below. [Or, watch on YouTube].

  [Or, watch on YouTube]: http://www.youtube.com/watch?v=eqw4zxqPelc

{% youtube eqw4zxqPelc %}
