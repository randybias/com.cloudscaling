---
author: Randy Bias
comments: true
date: 2013-03-27 17:51:00+00:00
layout: post
slug: service-resiliency-doesnt-always-mean-ha-or-cluster
title: Service Resiliency Doesn't Always Mean "HA" or "Cluster"
---

At the OpenStack Summit in San Diego last October, Dan Sneddon and I took the stage to dispel the notion that building a robust system automatically means "HA-mmers" or "cluster."

In fact, we made the point that the only way to build availability into elastic cloud deployments is to embrace alternative redundancy patterns with tools available in OpenStack. We then showed the audience how we do just that with Open Cloud System.

It doesn't take much for a cluster to become dramatically and incurably complex. There are a million ways to break. And when it breaks, it's a binary failure condition: it either works, or it doesn't. There's no in between. Effectively, you've built an operational nightmare. We even talked about some of the more epic HA failures of public systems in the past few years.

We talked about the scale-out mindset as the foundation for service resiliency. Service distribution, when built properly, leads to HA without compromise (resilient, stateless, scale-out). Examples of how to do this in OpenStack were followed with an explanation of how we did it in Open Cloud System (app proxies, IP LB, ECMP, RGP/OSPF/IS-IS)

The preso also includes a brief discussion of brokerless messaging with ZeroMQ.

Both the Slideshare deck and the video are embedded below. Let us know what questions you have &amp; we'll post answers below.

{% youtube VgpiD-QbW_M %}

<iframe style="border: 1px solid #CCC; border-width: 1px 1px 0; margin-bottom: 5px;" src="http://www.slideshare.net/slideshow/embed_code/14832750" height="427" width="512" allowfullscreen="" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>

[OpenStack Summit :: Redundancy Doesn't Always Mean 'HA' or 'Cluster'](http://www.slideshare.net/randybias/open-stack-designsummithapairsarenottheonlyanswer-copy)
from [Cloudscaling, Inc.](http://www.slideshare.net/randybias)
