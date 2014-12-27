---
layout: post
title: On Scaling out NodeJS in a Reliable Manner
date: 2011-02-06 18:15:03.000000000 +00:00
categories:
- Future
tags: []
status: publish
type: post
published: false
meta:
  _edit_last: '1'
  _wpcom_is_markdown: '1'
  tmac_last_id: '531409140074414080'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415078058;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:315;}i:1;a:1:{s:2:"id";i:356;}i:2;a:1:{s:2:"id";i:251;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

## Single-Thread I/O ##

Why this is good, separating I/O from CPU. Exception with large shared state,
i.e. YCS. Reliability and stress tests are critical. A single Javascript
context overhead per process.

Scaling to multiple cores involves multiple processes, handing off the socket
file descriptor and accepting the connection on the child process, letting the
kernel do the round robin. Note that there are other ways to scale out, but
this is the preferred way.

On spawn vs fork, i.e. describe Bene's patch.

## Do we need threads? Handing off CPU-bound workloads ##

WebWorkers to child process, not effective, need for multi-threading to fully
effectively leverage multi-core configurations, e.g. 64 cores. Discussion on
process vs thread based, and why we want threads.

## Adding Javascript ##

* Single threaded I/O: must ensure reliability, if the reactor comes down,
it's a BIG deal as thousands of accepted socket connections will reset. MTTF
must be very high. It comes down to V8 handling errors more gracefully and
allowing recovery.</li>
* CPU bound workload: running a separate Javascript context per thread. There
are two options, the V8-way or the-other-Javascript-engine way.

<li>V8 uses statics and, unlike other Javascript engines, none of the method
signatures passes the context along. We could move all statics in V8 into
a context object and pass it along in thread local storage when we call
::Lock.</li>
<li>Switch from V8 to a context-per-thread engine, e.g. JaegerMonkey or
JavaScriptCore. To allow compatibility with V8, we would need to hide the
Context object being passed along on every call to the engine. We would
create a V8-like API that does that magic behind the scenes using thread
local storage.</li>
<li>In either case, we'd have to do some similar fixes in NodeJS itself, as
most of the statics would need to move onto a separate global object.</li>

## Decoupling Reactor and JS ##

If JS drives the reactor, a JS-engine failure, kills the reactor.
