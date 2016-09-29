---
author: Randy Bias
comments: true
date: 2013-04-02 19:19:23+00:00
layout: post
slug: announcing-python3-compat-team
title: Announcing the Python3 Compatibility Team
---

Two weeks ago, I attended [PyCon]. I had a great time and it was an invaluable experience. It was striking how much one misses when they’re not running the latest Python release.

  [PyCon]: https://us.pycon.org/2013/

Now, I’m not so influenceable as to suddenly jump onto the [Python3] bandwagon just because I spent a couple days with other Python hackers. However, it was clear that the [OpenStack Foundation] and the project itself should do more to facilitate those projects seeking to enter the ecosystem, or even those already in the ecosystem, to develop code against Python3.

  [Python3]: http://docs.python.org/3/whatsnew/3.0.html
  [OpenStack Foundation]: http://www.openstack.org/foundation/

If we don't enable developers to write Python3 code, they'll have no choice but to write code against Python2.

As a result, I have since launched the [Python3 Compatibility Team for OpenStack]. Already, we have 24 members.  Our team’s mission is precisely as I above identified, to enable and support efforts by projects in the OpenStack ecosystem to use Python3. The scope of that effort is simply, for now, to migrate our libraries. No project in the ecosystem can run without dependencies and those dependencies, in and outside of OpenStack itself, must be compatible with Python3.

  [Python3 Compatibility Team for OpenStack]: https://launchpad.net/~openstack-py3-team

The first target for our efforts will be to introduce gating, following by an active porting effort of the [oslo.config] library. This library is fairly small and has few external dependencies, is used by almost all the projects, and is also the first library that has officially broken out of incubation. This will help limit the scope, provide a useful proving ground, and will also allow us to make a markable and noticeable difference.

  [oslo.config]: https://pypi.python.org/pypi/oslo.config

At least for now, there are no plans or intentions to port or attempt to port core projects such as Nova, Cinder, Quantum, Glance, or Swift. Our team effort will enable a transition path for those projects, should they choose to take it.

We’ll be meeting every-other week on Thursdays at 9am PST in \#openstack-meeting and have already had our inaugural meeting ([minutes]). Our next meeting is Thursday, April 4th. Following that, we ask all those interested also join the "[Python3 in OpenStack]" summit discussion in Portland.

  [minutes]: http://eavesdrop.openstack.org/meetings/python3/2013/python3.2013-03-21-16.06.html
  [Python3 in OpenStack]: http://summit.openstack.org/cfp/details/143
