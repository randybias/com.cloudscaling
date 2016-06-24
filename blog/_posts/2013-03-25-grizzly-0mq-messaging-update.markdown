---
author: Randy Bias
comments: true
date: 2013-03-25 20:31:00+00:00
layout: post
slug: state-of-the-q-zeromq-in-openstack-grizzly
title: State of the Q - ZeroMQ in OpenStack Grizzly
---

The ZeroMQ messaging driver for OpenStack, as an alternative to RabbitMQ and Qpid, was made available as an RPC plugin for Essex and officially introduced to OpenStack with the Folsom release.

Since then, we have deployed the driver at scale and have found bugs, we've reported them, and we've fixed them. Grizzly includes these fixes and some may make it back to Folsom as backports (they're already backported to our latest OCS builds). Bugs have also been found in eventlet where they've also been fixed.  Additionally, improvements have been made to the Matchmaker on which ZeroMQ greatly depends, those improvements are also reflected here.

I see Grizzly as having been a major stabilization release for the ZeroMQ driver. If we were Microsoft, this would be our SP1 (for ZeroMQ messaging).

Fixes and improvements:

  - Supports new Oslo-RPC envelope (<a href="https://github.com/openstack/oslo-incubator/commit/f1e5d569b6c9ceb6d7a4b338db9186e4f9c2fb7b">commit</a>)
  - ZeroMQ driver-specific envelope is now versioned.  (introduced with fixes for rpc envelope <a href="https://github.com/openstack/oslo-incubator/commit/f1e5d569b6c9ceb6d7a4b338db9186e4f9c2fb7b">here</a>)<a href="https://bugs.launchpad.net/oslo/+bug/1123709">
</a>
  - Notifications tested and supported. (<a href="https://github.com/openstack/oslo-incubator/commit/c4400ec172fe7a57cbf92dcdce365ddb1ab66bae">commit1</a>, <a href="https://github.com/openstack/oslo-incubator/commit/82f3691de3dbf9c18f8fa151db9d21837410a128">commit2</a>)
  - Workaround for file descriptor leakage due to Eventlet regression. (<a href="https://github.com/openstack/oslo-incubator/commit/f1b23c8077593334ec8bc94fcb40287b7d31f7a5">commit</a>)
  - Fixed a dead-lock that could happen in edge-case configurations. (<a href="https://github.com/openstack/oslo-incubator/commit/ab043101589a9167357ca317ca610a3f4144747c">commit</a> - <a href="https://bugs.launchpad.net/oslo/+bug/1097856">bug</a>)
  - Improved unit tests. - Thank you Monty!
  - Gating unit tests! - Thank you #openstack-infra!
  - Faster - only unpack replies on caller, no more deserialization in ZmqProxy (<a href="https://github.com/openstack/oslo-incubator/commit/b51a7241db53d87d780849563b99b5eee41761ba">commit</a>)
  - Faster - greenthreaded ZmqProxy (<a href="https://github.com/openstack/oslo-incubator/commit/ab043101589a9167357ca317ca610a3f4144747c">commit</a>)
  - Simplifications - such as replacing the MatchMaker lazypluggable and DIY for ZmqProxy.
  - Multiple "hosts" on one system for a single topic. (<a href="https://github.com/openstack/oslo-incubator/commit/6930432887f3551f88d08815fd04808fd15a07cc">commit</a>)
  - The *-rpc-zmq-receiver binary is now seeded from oslo's  bin/oslo-rpc-zmq-receiver to oslo (cross-project repo).

MatchMaker changes:

  - Dynamic matchmaking. ([commit]) - Grizzly’s Matchmaker required round-robin and fanout queues to be statically defined in a JSON file, or required deployers to provide a 3rd-party matchmaker module.  Grizzly now includes hooks to register and maintain a heartbeat to a datastore and/or service to maintain a host/topic registry.  A reference implementation utilizing Redis-based has been commited. File-based matchmaking is still available.

  [commit]: https://github.com/openstack/oslo-incubator/commit/cb26af207dbcea5fc88ad5f66da80fba5d76cb04

Open Issues for Havana:

  - Quantum and Ceilometer support. In Folsom, these projects abused private methods part of the AMQP modules. A blueprint led a way to an agreeable abstraction via a new public method, but it came late in Grizzly. Havana should support the new public method.
  - Merging or bridging the ServiceGroup API and the MatchMaker. Too much duplication of effort!
  - Moving the 'context' into the RPC envelope (rather than the ZeroMQ envelope)
  - Zero-Copy messaging to use references instead of data copies where possible. This is an optimization.
