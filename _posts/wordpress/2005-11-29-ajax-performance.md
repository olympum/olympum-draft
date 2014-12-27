---
layout: post
title: AJAX Performance
date: 2005-11-29 14:42:00.000000000 +00:00
categories:
- Architecture
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409308060495872'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

AJAX is the new pink. In fact, Web 2.0 could be the internet revolution that makes even Bill Gates wonder about the future of software. The enhanced usability in AJAX implies a couple of things for web applications.

<ul>
<li>Some of the controller logic is moved from the server to the client. Less CPU cycles on the server per page, more on the client.</li>
<li>Clients make more frequent requests to the server, but with significantly smaller payloads.  The business logic on the server is broken up into smaller, more self-contained XML services (SOAP, REST). In essence, same aggregate CPU, more I/O.</li>
</ul>
<p>Add to that a higher level of concurrency. More frequent, less expensive requests, same user, results in higher transaction rates, which will require more concurrent threads. More threads will consume more resources, both CPU and I/O.</p>
<p>During a simple AJAX revamping exercise, for the same amount of functionality, user CPU time is likely to be reduced on the server, and network I/O to go up. The extreme case with an AJAX MVC, and the server providing only web services, will actually reduce the CPU requirements on the server.</p>
<p>However, there are a few catches software architects should really start to consider:</p>
<ol>
<li>AJAX will increase bandwidth requirements on the server, and reduce the ability to scale up hardware to CPU saturation, increasing the average hardware cost per CPU cycle. In other words, AJAX is not a server efficient technology unless you revisit the data going back and forth.</li>
<li>Once the AJAX-night fever comes down, a next wave of web design will start to put more emphasis on orchestration and collaboration. Web services transaction management will start to be more mainstream due to additional client requirements, and stateful web services will appear (sadly?).</li>
<li>Current server tuning rules will no longer apply, given to changes in usage patterns. Multi-core architectures, such as Niagara and Power5 will be best placed to serve the increase in threading. Niagara being a lower power, high bandwidth chip, but not necessarily a fast CPU, will be one of the best architectures to run AJAXed applications.</li>
</ol>
