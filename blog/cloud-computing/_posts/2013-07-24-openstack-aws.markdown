---
author: Randy Bias
comments: true
date: 2013-07-24 14:29:02+00:00
layout: post
slug: openstack-aws
title: OpenStack's Future Depends on Embracing Amazon. Now.
wordpress_id: 6503
old_categories:
- Cloud Computing
- OpenStack
tags:
- amazon
- api
- aws
- Nova
- OpenStack
- Rackspace
---

## An Open Letter to the OpenStack Community:

## Our Future Depends on Embracing Amazon

<**UPDATE**: Please see [the follow up response](http://cloudscaling.com/blog/openstack/looking-in-the-mirror-a-response-to-my-open-letter/) to this letter .>

Dear Stackers, 

For three years, elements of the OpenStack community have arbitrarily and unfairly positioned OpenStack against incumbents, especially Amazon Web Services (AWS) and VMware (VMW). The practical expression of this view is that OpenStack should build and maintain its own set of differentiated APIs.

I’ve made no secret of my belief that this choice will harm OpenStack, and perhaps already has. Now, the issue has become urgent, and I hope to convince you to join me in advocating that OpenStack immediately and deliberately embrace the APIs and features of established public clouds. Doing so is critical to the success of a project that we all have labored to build. More importantly, doing so is precisely aligned with the [OpenStack mission](https://wiki.openstack.org/wiki/Main_Page).

To convince you, I will first explain the history that brought us to a differentiated API set. Then, we’ll look at why AWS and GCE domination of the public cloud is inevitable. I will debunk the fear, uncertainty and doubt surrounding legal issues of copying APIs, and finally, we’ll directly take on the nonsense about controlling of the “innovation curve” in cloud computing.

### How We Got Here

When OpenStack launched in the summer of  2010 there were no “native” APIs in one of the two components. Nova initially provided only the EC2 APIs. This part of the project, contributed by NASA, was focused on recreating a private cloud system compatible with EC2. The Rackspace APIs were added after the EC2 APIs and just ahead of the 2010 summer launch of the OpenStack project.(1)

Quoting the original [README](https://github.com/xtoddx/nova/blob/master/README.rst) from the Nova project:

You have come across a cloud computing fabric controller. It has identified itself as "Nova." It is apparent that it maintains compatibility with the popular Amazon EC2 and S3 APIs.
> 


Notice the lack of any  mention of “native APIs” in the Nova project description and compare it to today’s Nova [README](https://github.com/openstack/nova/blob/master/README.rst).

Swift (the other half of the project), used its own native APIs, which were created by Rackspace as part of their Cloud Files service, the origin of Swift’s code.

More concisely, OpenStack originated with “native” APIs, where one half was AWS compatible (Nova) and one half was Rackspace public cloud compatible (Swift).

Then, [Rackspace acquired ANSO Labs](http://allthingsd.com/20110209/exclusive-rackspace-to-acquire-anso-labs/) and it effectively “owned” the other half of OpenStack code contributors. More importantly, most of the project team leads (PTLs) who would make decisions about the overall technical direction of the project were now employees of Rackspace.

Around the time that ANSO Labs was acquired, the Rackspace API was [renamed](https://github.com/openstack/nova/commit/1e403e56dc1147ce3feea1b8931948bc35f23a44) to “nova-api” and this is what is now referred to as the “native API” of Nova.(2) This API is largely identical to the Rackspace Cloud Servers public cloud service API. It still is mostly this API today, deeply influencing the nomenclature of the project (e.g. “floating IPs” vs. “elastic IPs”) and to some degree the direction of Nova.

There is nothing “native” about the Nova API. In fact, calling the Rackspace Cloud Servers API the “native API” promulgates the notion that there is an OpenStack Nova API that is separate from Amazon’s. It’s now obvious that the original native API for OpenStack was in fact its AWS EC2 API.

### *We* Control OpenStack

The governance of OpenStack has matured since 2010 when the decisions described above were made. The [OpenStack Foundation](http://www.openstack.org), an independent organization, now guides the strategic and business aspects of OpenStack, while its developer base runs the project as a technical meritocracy.

In short, the community controls the direction of the project, and it’s time we advocate a public cloud compatibility strategy that is in all our best interests, not just those of a single, albeit substantial, contributor. Failing to make this change in strategy could ultimately lead to the project’s irrelevance and death.

### Amazon Dominates Public Cloud

It is clear that AWS (and quite likely GCE) will utterly dominate the public cloud race. But more importantly, who cares? Dominance by AWS and GCE does not mean that OpenStack fails. In fact, OpenStack is clearly [on a trajectory to “win” the private cloud race](http://www.slideshare.net/randybias/state-of-the-stack-april-2013), and a rapid embracing of Amazon will put OpenStack in the pole position to dominate hybrid cloud.

At Cloud Connect in February of 2011, I gave a [keynote](http://vimeo.com/21372341) outlining the “[two cloud story](http://cloudscaling.com/elastic-cloud/)” with numbers on the size and growth of AWS and Rackspace Cloud Servers. At that time, I believed Rackspace had a shot at success in the public cloud space because their annual growth rate put them in a dead heat with AWS: ~100% for AWS and ~90% for Rackspace.

But in the 2.5 years since then, much has changed. AWS’s growth has continued unabated, and GCE entered the race in earnest. Rackspace, meanwhile, faces declining growth velocity. If Rackspace earnings for Q2-Q4 of this year match Q1, they will have declined from that high of ~90% annual growth for their public cloud down to ~30% annual growth, a staggering decline in the past few years. See the following chart, which assumes that quarter over quarter growth in 2013 stays constant.

  
[![rackspace-yearly-growth-numbers (2)](/assets/media/2013/07/rackspace-yearly-growth-numbers-2-1024x619.jpg)](/assets/media/2013/07/rackspace-yearly-growth-numbers-2.jpg)

There is no public information about GCE’s growth, but I believe it to be on par with AWS. This is based partly upon learning that the level of interest in their service was so high that their wait list queue was longer than the customer list of most other public clouds actually in production. And that was while they were still in private beta.

Why bring up Rackspace public cloud’s sudden decline? Simply to illustrate that the available information shows that AWS and quite possibly GCE are the leading public cloud services and present an obvious alignment choice for the OpenStack community.(3)

### Amazon Controls the Innovation Curve in Public Cloud

In 2010, some argued that standardizing on the Rackspace public cloud APIs would allow OpenStack to control the innovation curve instead of Amazon. Since then, Amazon has continued to push new features into production at a breathtaking pace. They are, quite simply, in control of the innovation curve in public cloud. Every public cloud feature added by an AWS competitor is measured directly against what AWS has already built.

OpenStack can be in control of the innovation curve in private and hybrid cloud, but doing so requires that we support the services that are leading the innovation curve in public cloud. For OpenStack to dominate innovation in private and hybrid, it must embrace the public clouds to which enterprises want to federate.

### OpenStack Can Dominate the Hybrid Cloud Future

While [I once panned the term](http://cloudscaling.com/blog/cloud-computing/hybrid-clouds-are-half-baked/), I have long believed that private and public clouds needed to look similar and connect if we’re to have massive cloud adoption. We are now seeing enterprise customers demand a hybrid cloud solution: a private cloud connected to a public cloud so they can run workloads in both places and generally have choice and control that drive positive economics and business agility.

What is perhaps at contention is the idea that a set of public clouds based on OpenStack will arise to serve one half of this equation. The likelihood of such public clouds seems low to miniscule at this point. AWS and GCE already have position, global reach, rapid feature iteration and growth rates that establish their leadership. What can stop them? Frankly, there are no contenders on the radar. 

In a world where AWS and GCE dominate the public cloud market, private clouds that wish to provide a hybrid option must embrace these leaders.

All this leads to an inevitable conclusion: OpenStack’s future is predicated on driving hybrid cloud compatibility with the major public clouds, and those are AWS and perhaps GCE. If others arise, we should debate and evaluate embracing them only when their market position is established.

### Fear of Legal Action is Ungrounded

Because of the [Oracle vs. Google ruling](http://en.wikipedia.org/wiki/Oracle_v._Google) on the Java Virtual Machine vs. Davlik Virtual Machine, it’s likely impossible to protect a set of public APIs in court. 

Fear, uncertainty, and doubt on public cloud API protectability is complete foolishness. There is no legal basis for stopping the OpenStack community from copying the AWS and GCE APIs. Also keep in mind that Amazon’s APIs have already been copied. Their ability to succeed in a new legal action would therefore be compromised by the fact that they’ve not fought copying in the past.

### The *Entire* OpenStack Community Wins

Embracing Amazon serves the interests of all community members by positioning OpenStack as the best choice for enterprises and SaaS providers that want an ecosystem approach to public cloud, one in which their applications can move to the infrastructure best suited to the job at that time.

Put differently: if OpenStack-based public clouds embrace the major public cloud APIs, they put themselves in a position to benefit from the AWS ecosystem, allowing them to carve at pieces of the pie. Similarly hosting companies have the opportunity to sell hosted private clouds that are public cloud compatible to solve the the hybrid cloud problem for enterprises. In fact, this is probably the strategy that Rackspace should have been pursuing.

It is for this reason that Rackspace is also a winner under my proposal. They are in a unique position to deploy private hosted OpenStack hybrid clouds that are compatible with whatever public cloud the customer wants.

### The Time is Now: Embrace Amazon and the AWS APIs

The time has come for the OpenStack community to choose a public cloud compatibility strategy that will position the project for dominance in the private and hybrid cloud markets.

Time is of the essence. AWS is already dabbling with providing private AWS regions for the government (AWS GovCloud) and even specific agencies (CIA/NSA). It is reasonable to conclude that they might expand this program, threatening to dull OpenStack’s present opportunity. 

### My proposal is as follows:

1. Embrace major public cloud APIs

    GCE, AWS, Azure, and possibly vCloud

2. Rename the Nova API to the Rackspace Cloud Servers API

3. Create a new low level API(4) and move to the bridged API model

4. Expand testing and the work around [refstack](http://www.openstack.org/summit/portland-2013/session-videos/presentation/heat-refstack-a-reference-implementation-of-openstack)

    Refstack should focus on public cloud interoperability & hybrid cloud

5. Embrace existing AWS interoperability testing frameworks  

    The Cloudscaling aws-compat and the Eucalyptus eutester library are examples

Amazon and Google are our friends because they are spreading awareness and adoption of cloud computing. They are “making the pie bigger” for us all. Together, they are creating a rich and vibrant public cloud ecosystem, and OpenStack and can connect to it with a rich and vibrant  private cloud ecosystem. I want OpenStack to be the dominant hybrid cloud solution. Please help me make this a reality.

Sincerely,

Randy Bias

***

[1] For those interested, here is the [original check-in](https://github.com/openstack/nova/commit/d6c78d600091f476e360371df033be7eda1b749b) of the Rackspace (nee “Nova”) API by Todd Wiley of ANSO Labs at the time.  Note that the files are “rsapi” and “rackspace.py” NOT Nova.

[2] It looks like the rename happened 8/17/2010, so post-launch and pre-ANSO acquisition, which was February 2011.  All of the references to a Rackspace API were finally [removed](https://github.com/openstack/nova/commit/7a95f73ad7b295ddd2313152973c6da2c78fac76) in September 23rd, 2011.

[3] The last estimates were that AWS Elastic Compute Cloud (EC2) closed off 2012 with roughly 2B in revenue and 2M+ virtual servers, numbers that eclipse all other major clouds besides GCE, which should be considered the #2 public cloud already.

[4] A low level API without an opinion would have allowed for having multiple API “bridges” similar to how CloudStack has an EC2 API bridge to easily and cleanly support multiple higher level “opinionated” APIs with much less effort and with much higher levels of maintainability. Imagine Nova with the AWS, GCE, Rackspace Cloud Servers, and vCloud/vSphere APIs. That would have been straightforward using this kind of architecture. [OCCI](http://occi-wg.org/about/specification/) is a good example and a strong candidate.
