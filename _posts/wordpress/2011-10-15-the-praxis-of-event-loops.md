---
layout: post
title: The Praxis of Event Loops
date: 2011-10-15 15:27:47.000000000 +01:00
categories:
- Future
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409133703299074'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415511168;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:8;}i:1;a:1:{s:2:"id";i:315;}i:2;a:1:{s:2:"id";i:340;}}}}
  _wpcom_is_markdown: '1'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---
  
On a theoretical world, given the ability for a processor to run an
infinite amount of threads, we could prove the following statements
(no attribution purposely given): (1) If you do more CPU than I/O, use
threads; (2) If you do more I/O than CPU, use more threads. Which
would allow us to conclude with the following corollary: "_at full
utilization, threads and events have the same theoretical
throughput._" Such argument ignores **praxis** -- it is a purely
**theoretical** debate disconnected from the reality of scaling
services --.

<p>Yahoo! serves over 20 billion daily requests through it's edge
services (remote proxies and caches throughout the world). These
intermediate servers are doing pure IO workloads, handling slow client
IO and handing connections off to the origin servers through Yahoo's
pipes. It is critical that we minimize the CPU cost per connection to
be able to max the CPU at the max number of connections per host.</p>

<p>The hosts on Yahoo!s edge network run exclusively event loops, and
have been doing so for over a decade, originally with Inktomi Traffic
Server then with Yahoo Traffic Server, and now with Apache Traffic
Server, etc. The design throughout is the same: a few "master" event
loop threads, usually one per core, and a small pool of worker
threads. In total, a handful of 20~50 threads per server. With this
design, Yahoo! is able to scale to hundreds of thousands of
connections per server. It is currently still impossible, <em>in
practice</em>, to run a server with so many threads and still serve
data.</p>

<p>Another practical need for event loops occurs at the other end of
the serving stack. Resolving a search query follows a general pattern
of parsing and rewriting the query, followed by fetching potential
search results, and finally doing document re-ranking. The first and
last phases are CPU intensive. The fetch operation is purely an IO
workload that performs a scatter-gather operation which fans out to
hundreds to thousands of back servers holding the search index across
tens of columns. As a consequence, for every client connection, it's
possible to require one thousand upstream connections. When the
upstream index servers become slow, which is a common failure
situation, or perhaps in scenarios where we have to fetch data from a
remote data center, the number of connections in the system grows to
tens of thousands. It is also important that we keep all three phases
running on the same process to avoid serialization and transfer costs,
essentially forcing us to mix CPU and IO intensive workload. It is
currently still impossible, <em>in practice</em>, to perform this type
of data intensive processing without using event loops.</p>

<p>Unlike Yahoo's services, which combine an event loop with a handful
of threads per core, Node.JS design is a single-threaded event-loop
per core. For pure IO workloads this ensures the necessary simplicity
required to be able to design software that scales to thousands of
concurrent active connections, as long as nothing is blocking. I find
it unfortunate that some developers have not internalized this and are
trying to run CPU intensive applications using Node.JS. Inferring that
because these badly designed applications are a failure, therefore
Node.JS is a failure is an unnecessary and unfair generalization.
Node.JS has a field of <em>practical</em> applicability, and like any
tool, a seasoned practitioner should know when, and when not, to use
it.</p>
