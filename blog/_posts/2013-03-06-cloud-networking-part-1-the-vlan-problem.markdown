---
author: Randy Bias
comments: true
date: 2013-03-06 19:11:23+00:00
layout: post
slug: cloud-networking-part-1-the-vlan-problem
title: Cloud Networking - Part 1&#58; The VLAN Problem
---

This is the first part in a multi-part series discussing general networking patterns and problems in infrastructure clouds, gentle critiques of various existing networking approaches in stacks such as OpenStack and CloudStack, and recommendations on best practices.

This first article deals with the general topic of VLANs and more specifically the problems with traditional [hardware VLANs](http://en.wikipedia.org/wiki/IEEE_802.1Q) that leverage 802.1q.

## Extending VLANs into the Hypervisor is a Bad Idea

Significant problems arise when traditional 802.1q VLANs are extended down into a hypervisor such as ESX, Xen, or KVM.  At the heart of the matter are a number of assumptions that have traditionally held true of VLANs when they are used in a physical switch fabric, but that break down if the switch fabric is extended to software that runs locally on the hypervisor.

To bottom line it, once the switch fabric is extended to the virtual switch (aka vSwitch) in a hypervisor, there is a significant change in the security profile of a system.  Significant additional care needs to be paid to the configuration of your cloud in order to keep it secure.

Additionally, smaller clouds built with 802.1q-based VLANs may find themselves particularly challenged as they grow larger because of the need to run spanning tree protocol (STP).  STP fails over slowly and reduces your total available bandwidth by half.  In addition, most 802.1q friendly network architectures are extremely limiting in what they allow.

## 802.1q for Network Partitioning

Before exploring the security problem we should quickly explain how 802.1q VLAN tagging works. It's very simple actually. Switches are configured to have separate "virtual networks" for different tenants.  Ethernet frames originating from a particular port or MAC address have a 4-byte header (‘tag’) added which contains a 12-bit VLAN ID.

[![](/assets/media/2013/03/vlan-tagging.png)](/assets/media/2013/03/vlan-tagging.png)


The switch fabric is then smart about restricting the forwarding of that Ethernet frame to only other computers on the same virtual network.  This, in effect, provides basic network partitioning and is the de facto way in which different applications and datacenter tenants are isolated in most enterprise datacenters today.

This technique has worked for a long time now and has been mostly secure due to a [security through obscurity](http://en.wikipedia.org/wiki/Security_through_obscurity) benefit: attacker or hacker access to the switch fabric is very difficult as most of the switch operating system code is closed source and highly proprietary.

This has led to 802.1q VLANs being the accepted de facto approach for [network isolation](https://www.google.com/search?q=virtual+network+segmentation+for+pci&amp;aq=f&amp;oq=virtual+network+segmentation+for+pci) for various compliance purposes such as [PCI](http://en.wikipedia.org/wiki/Payment_Card_Industry_Data_Security_Standard) and [SOX](http://en.wikipedia.org/wiki/Sarbanes%E2%80%93Oxley_Act).

## The Extended Switch Fabric

In order to allow the VMs of different tenants to be on the same layer-2 (L2) ethernet segment or "virtual LAN" while being isolated from others on an infrastructure cloud, a common approach is to use 802.1q and to extend the switch fabric down to the hypervisor’s vSwitch. What this means is that the virtual switches in every hypervisor tag the packets coming out of the virtual machines and these tagged packets are simply fed upstream to the physical switch fabric.

It should be fairly obvious what the problem is now.  As you can see in the Ethernet frame diagram above, 802.1q has no security measures of any kind baked into the protocol.  You are simply adding a 12-bit number (0-4095) to the Ethernet frame.  Any switch can tag any packet with any number for any VLAN by default.

This means that if an attacker in a multi-tenant cloud were able to breach the hypervisor and gain root access, they would be able to join any VLAN in the entire cloud.  It would be as simple as reconfiguring the vSwitch of the VM they had control of to talk to each network segment.  Sniffing on the 'wire' and port scanning would give the attacker plenty of information about the tenants of each network and would facilitate a more deliberate attack.

It's an incredibly dire kind of breach where your entire cloud network is compromised and it flies somewhat in the face of expectations of both networking folks and security engineers who have long assumed that VLAN tagging is 'safe'.  Again, this assumption breaks down *because* of the extension of the switch fabric from the physical into the virtual world or hypervisors. This obviously also impacts SDN and software VLANs as well, but I'll talk about the particulars of those systems in a follow on article for this series.

## Defenses against VLAN Hacking

There is really only one approach that can be used to try and harden your switch fabric against a malicious attacker who has access to a hypervisor and it's vSwitch, but it isn't very robust and takes a level of sophistication and automation that doesn't exist in most clouds today.  Basically, once you trust the hypervisor switch, all bets are off if an attacker gains access.

The primary defense is to configure your physical switch fabric in such a way that VLAN tags are restricted.  In effect, it's a way to filter out unexpected VLAN tags from presumably untrustable hypervisors.  For example, if you say that VLANs 10, 20, 300, and 435 are on this port, ignore all other VLANs, you can restrict the attacker's access to just those four VLANs.

[![](/assets/media/2013/03/restrict-vlan-tags.png)](/assets/media/2013/03/restrict-vlan-tags.png)

Unfortunately, in a multi-tenant infrastructure cloud environment you don't know in advance which VLANs will be where or which tenants will be assigned to which VLANs.  It's a very dynamic environment.  This means that as part of the network provisioning process you would have to dynamically reconfigure your switch fabric every time you place a new VM.  This is exceptionally difficult and I know of very few who have been wildly successful at doing this.  I know of zero who have done it in a vendor neutral manner.

Because of the difficulty, most clouds simply tag all VLANs down to all hypervisors, which again introduces the core security problem where an attacker has access to all tenant networks when the hypervisor is breached.

## VLAN &amp; Network Topologies

Taking aside the security issues, which are certainly scary as is, running VLANs across your switch fabric requires using spanning tree protocol [STP](http://en.wikipedia.org/wiki/Spanning_Tree_Protocol"). [STP is not your friend](https://www.google.com/search?q=spanning+tree+protocol+evils&amp;aq=f&amp;oq=spanning+tree+protocol+evils). It fails over slowly (30-50 seconds), requires lots of tuning, and has historically been extremely brittle.  This is reflected in the numerous updates to the technology to try and make it more robust like rapid spanning tree protocol (RSTP), per-VLAN STP (PVST/PVST+) , and multiple spanning tree protocol (MSTP).

Additionally, typical STP environments block half of the links, [cutting your total switch fabric bandwidth in half](http://etherealmind.com/bisectional-bandwidth-l2mp-trill-bridges-design-value/). That means typical STP environments block half of all redundant links, cutting your aggregate bandwidth by 50%.

This is In comparison to a typical ISP backbone or network architecture, which does not require bridging 802.1q VLANs between sites or running STP.  These network architectures instead are fully routed layer-3 (L3) network topologies using equal cost multi-pathing [ECMP](http://en.wikipedia.org/wiki/Equal-cost_multi-path_routing) for load balancing across multiple links.

This is why people love the idea of SDN and L2 over L3 (L2oL3) networks.  You can run a scalable L3 network, but get the VLANs we all know and love, but in a more scalable manner. This is the notion of “software” VLANs that I will cover in another posting.

The bottom line though is that VLANs and STP significantly impact your options when it comes to your networking topology, impact total bandwidth, and may actually reduce uptime due to brittleness.

## Summary

The primary point of this lead-in article is to point out that traditional enterprise datacenter networking techniques have assumptions that are probably invalid in cloud environments (e.g. VLANs are good security enforcement mechanisms).  We are in the midst of a series of significant advancements in networking that will move the traditional complexity in network architectures out into a ‘virtualized’ environment, while simplifying the underlying physical networking fabric.  VLANs are just one area that needs to be revisited.
