---
layout: post
title: Composable and Concurrent
date: 2009-04-23 15:00:31.000000000 +01:00
categories:
- Future
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409167895232514'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1414945836;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:315;}i:1;a:1:{s:2:"id";i:245;}i:2;a:1:{s:2:"id";i:313;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

On my previous entry <a href="/future/on-language-polyglotism/">on the
present and future of programming languages</a>, I briefly covered on
the reasons I think it is important to be looking at this problem now.
I though I would expand the discussion.

<p>The laws of physics that we know have stopped our ability to make chips significantly faster today, and rather hardware manufacturers now need to place more and more cores in one die. The result as software developers is that we are now faced with computers with multiple cores and multiple CPUs. It is now the norm to find computers with 2 cores, and most servers are now 4 or 8 core machines.</p>
<p>Historically, <a href="http://www.gotw.ca/publications/concurrency-ddj.htm">developers lived on the free lunch</a>, and with time they knew code would run faster, since clock speeds would get faster. Chips will still continue to get faster in the future, but marginally what we've seen over the last 18 years. Today, it's not about running faster, but having more transistors. And what once was a good programming paradigm for the single core, it's not valid any longer for the multi-core situtation.</p>
<p>Here is where concurrent programming is born. Writing software that scales to multiple cores with the current programming paradigms is hard. The main mechanism we know is the usage of threads, and locks to protect shared estate between threads. It is a model somewhat understand by developers, but that it is however extremely hard to get right.</p>
<p>On the server-side, programming languages that can only leverage one core are going to have a really hard time to compete in the future. Programming languages that have adopted the thread-per-request model are better placed, but will nevertheless face a wall at some point because they rely on locks to operate to protect the transactionality of shared state. Multi-threaded programming and locks are not scalable, mainly because they are not <em>composable</em>.</p>
<p>Building composable software really requires us to move away from sharing state. Working with immutable data structures, and immutable containers, allows us to avoid state, hence allowing modularity and composability (the core principle of software development for the last 35 years, and the philosophy of UNIX tools). But working with immutable data goes against extensibility principles in object oriented programming.</p>
<p>There are a few paradigms that have been in the research arena for the last 10 years and are now finally being adopted. These paradigms take the shape of message passing, parallel programming and functional programming. Functional programming languages are naturally parallel and use immutable data. Unfortunately functional programming languages are not mainstream, and most functional languages that have been successful (Haskell and Lisp) actually allow mutable structures. Erlang however is an exception. Erlang is naturally parallel, uses only immutable data, and is based on message passing. Erlang is a good language to solve the concurrency programming paradigm.</p>
<p>The question though is whether adopting a language like Erlang would make sense for most organizations. Rather, some may argue that evolving the abstraction of concurrency into the current leading programming languages is the way forward. I'd disagree since this is somehow what Scala does, but given that it lives in a JVM, with threads and locks, and using libraries that use threads and locks, it's unlikely new language constructs will allow existing code bases to be fixed. To me, Erlang looks like a much better choice. It's a proven choice and with many years of history.</p>
