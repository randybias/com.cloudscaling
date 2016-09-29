---
author: Randy Bias
comments: true
date: 2013-07-01 12:18:23+00:00
layout: post
slug: an-openstack-security-guide-in-five-days
title: An OpenStack Security Guide in Five Days
---

![](/assets/media/2013/07/openstack-security-guide.png)

Last week, I had the privilege of being involved in the authorship of a book. It was an intense and amazing experience and I'm still surprised that it worked, that we successfully outlined, wrote, and edited a book in only 5 days!

Our outcome was the [OpenStack Security Guide], a 154 page instructional on securing cloud deployments. This was a collaboration of individuals from Cloudpassage, Cloudscaling, HP, Intel, John Hopkins University Applied Physics Lab, the NSA, Nebula, Nicira (VMware), Rackspace, and RedHat.

  [OpenStack Security Guide]: http://justwriteclick.com/2013/07/01/book-sprint-for-openstack-security-guide/

In writing, we managed to squeeze in practical guidance on configuration topics that were previously undocumented or otherwise "hidden" features, such as using SSL client certificates for MySQL authentication. (Thanks <a href="https://twitter.com/mathrock">Nathanael Burton</a>!)   We also found a number of feature requests, questions-to-investigate-later, plus some serious and not-so-serious bugs.

I note, most of the feature requests, concerns, and bugs were found in the first day. Many would not have surfaced had we not had had this mix of vendors and personalities together in the same room. We would not have had nearly the same amount of energy should we have attempted this over the wire. It reminds me that we as a community would do well to continue various sprints and in-person events, lest we forget the value they bring.

Ultimately, I believe our book accomplishes a reasonable balance between scope and depth. This was difficult because several topics could be books in and of themselves.  It is impossible to be entirely happy with any creative work, but I'm pleased with our output. There is plenty of room for additional insight, especially when it comes to topics we know we couldn't scope -- we were too light on storage and didn't cover Compute Cells at all. However, we'll be releasing the book as Creative Commons and it will be put into 'git' as a living project, so we welcome future community participation.

Finally, I really need to thank [Adam Hyde] in particular for bringing his expertise to this exercise; Without him, we couldn’t have done this. Additionally, I thank [Bryan Payne] (Nebula) and [Robert Clark](HP) for their efforts in making this come together, [Keith Basil] (RedHat) and [Ben de Bont] (HP) for both their efforts and footing the bills, and everyone else with whom I shared, “an overly air-conditioned room” for 5 days.

  [Adam Hyde]: http://www.booksprints.net/
  [Bryan Payne]: http://www.bryanpayne.org/bio/
  [Robert Clark]: http://uk.linkedin.com/in/clarksecurity
  [Keith Basil]: http://www.linkedin.com/profile/view?id=6102994
  [Ben de Bont]: https://twitter.com/bendebont

The OpenStack Security Guide is immediately available for download as ePub. Soon, we will be making HTML and PDF versions available for download. A printed edition will also be available.

Download: [OpenStack Security Guide]

  [OpenStack Security Guide]: http://docs.openstack.org/sec/
