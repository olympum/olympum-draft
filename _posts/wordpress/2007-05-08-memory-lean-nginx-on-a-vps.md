---
layout: post
title: Memory-lean nginx on a VPS
date: 2007-05-08 16:32:48.000000000 +01:00
categories:
- Linux
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409252532097025'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415333186;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:97;}i:1;a:1:{s:2:"id";i:68;}i:2;a:1:{s:2:"id";i:315;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I spent this weekend testing and installing nginx and I have said Adios to Apache! Let me tell you why I have done that.

<p>I am running this blog on a <a href="https://manage.slicehost.com/customers/signup?referrer=49029804">slicehost.com</a> 256Mb Xen VPS, using WordPress. I have been using Apache 2.2 for almost a year now without any problems. But recently I deployed a little Ruby on Rails application using mongrel for my wife's business, and then suddenly I ran out of memory.  Each Apache worker was easily taking 15 to 20Mb, even with a really cut-down configuration and built on Gentoo. With three Mongrel backends and the MySQL server I was starting to swap to disk.</p>
<p>I tried FastCGI instead of Mongrel, but it only cut down from about 50Mb to 40Mb for each process, not enough really to make a difference.  I had to trim the fat out of the web server.</p>
<p>So  about dropping Apache. First I considered Pound as a load balancer, but given that I would also still need a web server for static content in Rails (not wanting to serve that with Mongrel) I decided to look for alternatives.</p>
<p>Lighty and FastCGI tests did not even complete, so I gave up on Lighty. The FastCGI processes were becoming Zombie for some unknown reason.</p>
<p>Then I tried nginx. I have 5 workers, each consuming around 3Mb. Wow ... I call that Spring savings.</p>
<p>nginx is sending all blog traffic to a couple of php-cgi handlers. I tried both TCP and Unix sockets, but went for TCP since I was getting dropped requests and stalling processes for Unix sockets. php-cgi is not very fast, but it's stable and it has a reduced memory footprint.</p>
<p>Then nginx is acting as a reverse proxy and balancing across 3 Mongrels. I tried also FastCGI, but again it's not stable.</p>
<p>And man is this thing flying or what!? I have enough memory spare to make MySQL happy. Plus I am caching a lot of Rails generated content that nginx serves happily.</p>
<p>Now, some numbers from Apache Benchmark (running on Linux 2.6.16.29-xen #3 SMP, x86_64 Dual Core AMD Opteron(tm) Processor 265 AuthenticAMD GNU/Linux, Xen host with 256Mb):<br />
nginx + pure HTML content:</p>
<p><code><br />
Concurrency Level:      50<br />
Time taken for tests:   0.96657 seconds<br />
Complete requests:      1000<br />
Failed requests:        0<br />
Write errors:           0<br />
Requests per second:    10345.86 [#/sec] (mean)<br />
Time per request:       4.833 [ms] (mean)<br />
Time per request:       0.097 [ms] (mean, across all concurrent requests)<br />
</code></p>
<p>nginx + php Wordpress home page (not cached, no APC):<br />
<code><br />
Concurrency Level:      50<br />
Time taken for tests:   192.387414 seconds<br />
Complete requests:      1000<br />
Failed requests:        0<br />
Write errors:           0<br />
Requests per second:    5.20 [#/sec] (mean)<br />
Time per request:       9619.371 [ms] (mean)<br />
Time per request:       192.387 [ms] (mean, across all concurrent requests)<br />
</code></p>
<p>nginx + mongrel (not cached):<br />
<code><br />
Concurrency Level:      50<br />
Time taken for tests:   8.290116 seconds<br />
Complete requests:      1000<br />
Failed requests:        0<br />
Write errors:           0<br />
Requests per second:    120.63 [#/sec] (mean)<br />
Time per request:       414.506 [ms] (mean)<br />
Time per request:       8.290 [ms] (mean, across all concurrent requests)<br />
</code></p>
<p>Sure, it's not a scientific test by any means, but it tells you something. And so far, no complains. If I ever outgrow the server, I can always get Pound on front of a couple of nginx web servers.</p>
