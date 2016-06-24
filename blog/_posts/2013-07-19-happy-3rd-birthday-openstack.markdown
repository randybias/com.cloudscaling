---
author: Randy Bias
comments: true
date: 2013-07-19 22:41:00+00:00
layout: post
slug: happy-3rd-birthday-openstack
title: OpenStack's Incredible Testing System is Behind Its Continued Success
---

<a href="http://cloudscaling.com/blog/cloud-computing/openstack-at-3-this-is-what-winning-looks-like/">Happy 3rd Birthday, OpenStack!</a>


I want the community to know how integral the continuous integration (CI) system ([TripleO]), plus integration tests ([Tempest]), plus unit tests (per project), are to our success.  Previously I [interviewed Monty Taylor] on this topic and he had a ton of fabulous insight to share on how the CI system works.  However, in looking back on the last three years and trying to understand why OpenStack continues to grow and hit every milestone, I think we should “do the numbers.”

  [TripleO]: https://wiki.openstack.org/wiki/TripleO
  [Tempest]: https://github.com/openstack/tempest
  [interviewed Monty Taylor]: http://engineering.cloudscaling.com/stacker-voices-monty-taylor-hp/


First up, notice the total number of unit and integration tests, which are well over <del>13,000</del> 15,000.  And due to lack of time, I am even missing a few key projects like <del>Swift</del>, Ceilometer, and <del>Heat</del> (will try and update soon!). (_UPDATED_: Graphic below updated to include Heat and Swift.)

[![](/assets/media/2013/07/happy-3rd-birthday-openstack-1.png)](/assets/media/2013/07/happy-3rd-birthday-openstack-1.png)


This is impressive, but perhaps most impressive is observing the trajectory of the creation of unit tests.  Just looking at Nova you can see that the community has been hard at work over the last three years adding test after test:

[![](/assets/media/2013/07/happy-3rd-birthday-openstack-2.png)](/assets/media/2013/07/happy-3rd-birthday-openstack-2.png)

This is incredible velocity and it really tells us about the commitment of the OpenStack community to deliver a high quality, production-grade, Cloud OS kernel.

More importantly, the OpenStack infrastructure team’s continuous integration system is deploying and testing OpenStack over 700 times a day using the Tempest integration tests, which have doubled in the last year:


[![](/assets/media/2013/07/happy-3rd-birthday-openstack-3.png)](/assets/media/2013/07/happy-3rd-birthday-openstack-3.png)


This is why we are able to move so fast and why no other Infrastructure-as-a-Service (IaaS) open source software development community will be able to catch us.

From the Cloudscaling engineering team:  thanks so much for the continuing hard work!
