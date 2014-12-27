---
layout: post
title: Nodes and Jetties
date: 2010-07-09 05:59:20.000000000 +01:00
categories:
- Future
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409153118703616'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415411119;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:313;}i:1;a:1:{s:2:"id";i:356;}i:2;a:1:{s:2:"id";i:347;}}}}
  _wpcom_is_markdown: '1'
  _edit_last: '1'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I am intrigued by node.js. Others are not so much. So they ask me, why node.js, why not Jetty, or Netty, or ... ? Others say, and Twisted, and EventMachine? The core of the answer lies in a simple not well understood truth: concurrent programming is really hard. Concurrent programming using threads and locks to shared memory is <em>extremely</em> hard. Most programmers get concurrency wrong, since they don't quite realize that threads actually execute <em>simultaneously</em>.

<p>Functional programming languages have long understood this, and designed mechanisms to avoid the risk of a programmer getting it wrong, such as immutable data structures (take a look at java.lang.String, designed by Lee Boynton, a true Lisp guy), or message passing (erlang).</p>
<p>Surprisingly, another line of programming has ended up in the same place. PHP can be deployed multi-threaded on Apache, but unfortunately most native libraries are <em>not</em> thread safe, so one ends up running processes as workers. Similarly, Python has the GIL, and Guido has no interest in fixing that. And yet, PHP and Python scale really well using processes.</p>
<p>So, here's the interesting bit about node.js. It's written on a functional programming language, Javascript, and provides a reactor server (remember POSA2?) on a single thread! I hear you say, how does it scale to multiple cores? It does not.</p>
<p>A single thread is only able to utilize one CPU. Even though most web apps are initially I/O bound, at some point programmers somehow manage to make them CPU bound (such as marshaling and wrangling JSON and XML). This will limit the scalability on the single process. In order to scale beyond 1 core, two possibilities exist. Right now, one would need to launch one node.js process per core, and then setup a load balancer. In the future, launching the processes needs to be done inside node (maybe this is fixed in the future?). The second option, which might also be implemented based on the node.js web site, is to adopt the Web Workers spec.</p>
<p>Now, because of the (single) threading model, response times are fairly unpredictable. One would expect a Java server on an async stack, such as Jetty, to provide more consistent response times, as it uses multiple threads. <a href="http://praxx.is/post/486034949/comet-with-bayeux-node-js-vs-jetty-and-cometd">A test</a> corroborates such hypothesis (look at the curve distribution for node.js vs jetty).</p>
<p>At the same time, because of the (single) threading model, memory usage is very low in node.js,  compared with Netty, or Jetty, where as a result of being multi-threaded, memory usage will be higher for the same load and latency. A <a href="http://news.ycombinator.com/item?id=1454722">discussion</a> on ycombinator seems to be along these lines. I am of the opinion that being able to run both on low and large memory profiles is critical to becoming successful, especially as many developers run their code in shared hosts.</p>
<p>If you have followed me this far, putting memory aside as that can be shared on the heap, you will then conclude that a multi-threaded Java-based async I/O server, like Jetty, should be better that node.js. And I would agree, only if it was not Java.</p>
<p>So here's the deal. Except a counted number of exceptions, Java libraries carry significant legacy of the wrong kind of concurrent programming, either abusing or ignoring locks. Either they do not scale to multiple cores, or they corrupt integrity of state. And this will continue to be a problem, since Java does not prevent bad programming practices in a concurrent setting. But there is a light: using the JVM, ignoring Java and most existing Java libraries.</p>
<p>Building new libraries for the JVM that are truly designed for concurrency requires using the right abstractions, and this is where functional programming comes into place. There are three key functional programming language contenders to the JVM: Javascript (Rhino), Scala, and Clojure.</p>
<p>First, there is Javascript, with Rhino, Mozilla's Javascript implementation for the JVM. <a href="http://www.ringojs.org/wiki/">Ringo</a> is a nodejs alternative based on Rhino. Unfortunately, Rhino is slow and quite a memory hog. Additionally calls in Ringo are blocking, which defeats the programming model. And Ringo uses the same Java libraries that were not coded with concurrency in mind. Compared to nodejs, Ringo has no community (a quick scan reveals 9701 messages in the node.js mailing list in 12 months of usage, against only 181 in 2 years of usage).</p>
<p>Next, come Scala and Clojure. Both are very intriguing, perhaps Clojure being more of my taste. For Clojure, we now have <a href="http://github.com/ztellman/aleph">Aleph</a>, a thin Netty wrapper. On multi-core, it seems to beat node.js latency and throughput wise, at the cost of memory. And Clojure allows message passing, immutable data structures, ala Lisp, all transparently mapped onto threads. Beautiful I say.</p>
<p>But Scala and Clojure are not Javascript. Javascript attracts many developers from the browser world, it provides a consistent event-driven programming paradigm for both server runtime and client runtime. Eventually, this pushes most UI logic to the browser, and leaves the server as a smart data source. As much as I find Clojure extremely exciting, I don't think it can realistically compete with Javascript.</p>
<p>So, realistically, only node.js is a viable alternative today. Maybe Clojure truly succeeds, and a Clojure based async I/O server appears. But for now, node.js is more interesting.</p>
<p>But don't get me wrong: node.js is very young, truly bleeding edge, and needs substantial work. Some of that work will make it easy for applications to scale beyond one core. Scaling beyond one core will improve consistency in response times. But given the vibrant community and excitement (and hype) around node.js, I am fairly confident this will happen.</p>
