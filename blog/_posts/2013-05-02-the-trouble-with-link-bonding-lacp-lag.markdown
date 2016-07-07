---
author: Randy Bias
comments: true
date: 2013-05-02 19:28:00+00:00
layout: post
slug: the-trouble-with-link-bonding-lacp-lag
title: The Trouble With Link Bonding (LACP, LAG)
---

One of our favorite sayings at Cloudscaling is "Simplicity Scales." This saying has a slightly-less-well-known coda, "Complexity Fails."

Let's walk through a real-world example of this.

## Background

In Open Cloud System (OCS), our high-availability (HA) strategy for services that have persistent datastores is to use a UCARP IP to make sure that one and only one of the backend servers is active at any given time. Then we replicate data between all the backend servers so that if one fails, another can take over the UCARP VIP and the cloud continues operating normally. UCARP works basically like VRRP - multiple devices share a virtual IP address (VIP) and communicate using CARP to figure out which one of them should be active at any given time.

The typical server in an OCS installation has four NICs: one (1G) for hardware management (IPMI), one (1G) for systems management (PXEbooting, chef), and two 10G NICs. In our canonical network design, one of these 10G NICs is used for intra-cloud traffic between VMs and storage resources, and the other is used for external access for VMs to talk to the Internet (or other resources outside the cloud).

Here is a diagram of the standard network layout without bonding.

[![](/assets/media/2013/05/the-trouble-with-link-bonding-lacp-lag-1.png)](/assets/media/2013/05/the-trouble-with-link-bonding-lacp-lag-1.png)

This is a simple and well-understood network design, easily implemented with standard networking models that have been around for decades. But there's another option for how OCS can be deployed: using bonded interfaces on the servers and port channels on the switches to take those two 10G NICs and make them appear as a single 20G network link, and pass both intra-cloud and external traffic across that higher-bandwidth virtual link. Many of our customers have preferred this option, which in theory provides higher burst bandwidth and greater resilience to failure of a NIC.  Bonding sounds great, right?

Diagram of the network architecture with bonding.

[![](/assets/media/2013/05/the-trouble-with-link-bonding-lacp-lag-2.png)](/assets/media/2013/05/the-trouble-with-link-bonding-lacp-lag-2.png)

## The Trouble Begins

Let me tell you a story. It's kind of a detective story. Like everything else in OCS, we do extensive testing of our HA/failover solutions, and during such testing we discovered some odd behavior when running in bonded interface mode. In most of our tests, failover worked great. When a node failed, the other node would take over. Because everything had been replicated from the active node, no data was lost. When the failed node comes back up, it's supposed to see the broadcasts from the existing master and join the cluster as a backup. This happened most of the time in our tests, but in a certain environment we saw the wrong behavior, where a failed node would come up and take over as master. In some cases, this could happen before replication had finished, which is obviously a big problem. After a ton of time spent debugging and a lot of red herrings, we finally figured out what was happening. If you use the default values for UCARP configurations, you get the following behavior when a node comes up and joins an existing cluster:

  - new node listens for 3 seconds for an announcement from an existing master
  - if the new node does not hear such an announcement it promotes itself to master
  - also important, if a master node hears an announcement from another master, it will demote itself to backup IF the other master has a numerically higher IP address

Here’s what was happening. During the boot process on the new node, it was taking several seconds (more than three) for the port channel on the bonded interfaces to be setup between the server and the switch - until that happened each port had link, but no frames (or packets) were being passed. During this time, UCARP was starting and listening for announcements - announcements that it couldn't see because they come over the bonded interface, which wasn’t working yet. After three seconds the node was declaring itself a master, then the port channel would finish coming up and now both the new node and the previous master see announcements from a second master. Because the new node has a numerically lower IP address the other master demotes itself and you wind up with the new node becoming master - potentially before it has replicated data back over from the previous master.

Following diagram depicts UCARP under normal conditions.

[![](/assets/media/2013/05/the-trouble-with-link-bonding-lacp-lag-3.png)](/assets/media/2013/05/the-trouble-with-link-bonding-lacp-lag-3.png)

And under failure conditions.

[![](/assets/media/2013/05/the-trouble-with-link-bonding-lacp-lag-4.png)](/assets/media/2013/05/the-trouble-with-link-bonding-lacp-lag-4.png)

We never saw this behavior with unbonded interfaces, because there is no setup delay for the network in that case. The new node comes up, starts UCARP, hears the announcement from the previous master, and joins the cluster as a backup just like it's supposed to. We also didn't see this behavior with all models of network switches - some set up the port channels faster than others, and as long as it takes less than three seconds for the port channel to start passing traffic to the node, we see the proper behavior. We only saw it with a certain network switch that took more than three seconds, and we only had that switch in one test environment.

## Bringing It Home

So back to "simplicity scales, complexity kills." Interface bonding and port channels are newer technologies than basic switching and routing, and their implementation is more complicated on both the server and the switch sides. Because they are newer and more complex, the implementations from one vendor to another differ in significant ways (and have different bugs). In this case the complexity introduced by bonding introduced a new failure mode that manifested in way that is extremely hard to diagnose. Relying on simpler (and older) technologies can prevent having to deal with these kinds of hard-to-diagnose problems. For example, in other parts of OCS we use ECMP at layer 3 to provide HA to servers. This is a time-tested and well-understood mechanism that has been used by ISPs for HA for decades. We're planning on switching our existing UCARP implementations to such a mechanism in the future, for what should by now be obvious reasons. :)


## The Moral Of The Story: Keep It Simple

The worst part about this story is that by adding something that was aimed at making the system more reliable (redundant NICs) we introduced a new failure mode (likely multiple new failure modes) that wound up making the system less reliable. This is unfortunately a common theme with HA strategies. What appears at first glance to be a great idea has unexpected (and often negative) consequences on the overall system. The best way to avoid this is to use the simplest and most time-tested strategies you can to keep your systems up and running.

Keep it simple, people. Simplicity scales.
