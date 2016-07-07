---
author: Randy Bias
comments: true
date: 2013-02-06 19:39:00+00:00
layout: post
slug: elastic-cloud-infrastructure-101
title: Elastic Cloud Infrastructure 101
---

It’s my sincere pleasure to welcome you to the opening post of “Simplicity Scales,” the Cloudscaling engineering blog.

Historically, we’ve kept quiet about the details of our approach to building software and architecting elastic cloud infrastructure, but that changes now.  This blog’s mission is to engage the OpenStack development community and non-OpenStack cloud architects everywhere in a discussion about the variety of technologies and approaches we can take to solve hard problems related to elastic cloud computing.  Examples of technology areas we want to talk about:


  - Nova networking, network architectures, hypervisor networking, &amp; software-defined networking (Quantum, SDN)
  - OpenStack internals, open source software that works well with OpenStack
  - Approaches to managing hardware and organizing cloud infrastructure
  - Infrastructure security issues, security in OpenStack, hypervisor-related security challenges, and how “distributed software” impacts security generally
  - Scale-out storage approaches, measuring and managing IOPS, and comparison of storage technologies generally
  - Deep dive explanations of how Open Cloud System (OCS) solves some of these areas

Our slogan in engineering at Cloudscaling is “simplicity scales,” which inspired the name of this blog.  We fundamentally believe that the simplest solution is always the best and that it takes more effort to simplify than complexify.  More importantly, we have seen firsthand how systems built from lots of complex parts have more edge cases and are difficult to maintain and scale.

By scale, we mean the ability of an elastic cloud to grow elegantly and predictably. Elastic [cloud computing was brought to us by cloud pioneers like Amazon and Google]. Very few clouds will ever be that large, but what cloud system wouldn’t embrace the learnings of these pioneers?  The lessons of building at scale seeded the elastic cloud computing revolution and now it’s time to bring those lessons home to inform and guide the next wave of information technology.

  [cloud computing was brought to us by cloud pioneers like Amazon and Google]: http://www.cloudscaling.com/blog/cloud-computing/the-evolution-of-it-towards-cloud-computing-vmworld/

This blog is therefore about Cloudscaling’s engineers, engineering culture, and perspective on building elastic infrastructure clouds that don’t suck.

Tell your friends, follow the RSS feed, and join the conversation.
