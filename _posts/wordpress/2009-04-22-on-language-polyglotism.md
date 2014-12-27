---
layout: post
title: On Language Polyglotism
date: 2009-04-22 22:54:19.000000000 +01:00
categories:
- Future
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409168054231041'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I believe being a polyglot is nothing but an advantage, and that
polyglots are normally the best programmers. As a matter of fact, I
challenge myself to learn a new programming language every year. Last
year it was Scala, this year I've started learning and writing some
Erlang (and yes, there is a pattern here for functional programming
languages).

<p>One of the reasons I like learning programming languages is a drive to reach the Holly Programming Grail: I find most fascinating discovering which language is better suited for which task. In other words, some languages excel at tasks where other languages fail. An organization could decide to allow all those languages to exist, and if we were doing best-of-breed in every problem domain, we would end up with a language soup. So the question then is, is such soup good or bad? In other words, when we think about developing Internet applications: which and how many languages should an organization use?</p>
<p>There are two factors to consider in choice of language choices (assuming the language choice is functionally the best choice for solving the problem at hand): talent and operations.</p>
<p>Talent is truly an interesting one. Whereas a startup can possibly afford to pick more exotic languages based on their goodness, large organizations can do less so because of talent. This is because A-class developers will excel in any language, and usually A-class developers are polyglots. But one can only hire so many A-class developers, and eventually you end up growing into B- and C-class developers. Your ability to maintain software at that point really depends on your C-class hiring pipe. Pick a rare language choice, and you are calling for trouble.</p>
<p>Operations is very different from talent. Here the size of the company also matters. Developer cost will be the starting cost, but as the business becomes successful operational cost becomes the key driver (specially in consumer Internet applications). In a way, you want to pick the language choices that drive your productivity higher, and later slowly move into reducing your operational cost.</p>
<p>If you follow me, you'll notice talent and operations are conflicting today. Java is the mainstream programming language worldwide, i.e. A-, B- and C-class talent is widely available, yet scaling Java horizontally at linear cost is difficult. On the opposite end, Erlang is a good choice for distributed concurrency and scaling linearly, yet B- and C-class talent is difficult to find.</p>
<p>I used to advocate the JVM as the minimum host environment, yet allowing language choice across the stack. As long as it could run on the JVM and I could manage it, any language was fine. One could run the complete stack on a JVM. The presentation tier in JRuby, Jython, P8 or Caucho's PHP implementation. The application logic and persistence in Java or Scala. The batch computing in Scala. But it just does not work that well. Even though Scala has the artifacts to work, the JVM and the runtime libraries don't. Shared memory, native threads and locks means the JVM will be more expensive to scale and operate on the long run. The JVM is a feasible, stable and proven alternative, yet it is an expensive choice (in operational cost and probably lost opportunity because of slower agility).</p>
<p>Given this context, my language choices would be:</p>
<ul>
<li><em>Conservative</em> stack, which gets the job done well enough, can be operated, and you can get accessible talent.
<ul>
<li>Frontend: PHP</li>
<li>Application Logic: Java</li>
<li>Persistence: Java and C/C++</li>
<li>Batch: Java</li>
</ul>
</li>
<li><em>Medium Risk</em> stack, that addresses some of today's shortcomings, but reduces the talent pool:
<ul>
<li>Frontend: JRuby on a JVM, with Merb</li>
<li>Application Logic: Scala on a JVM, with Jersey</li>
<li>Persistence (non-relational): Scala on a JVM</li>
<li>Batch: Scala, with Hadoop</li>
</ul>
</li>
<li><em>High Risk</em> stack, forward looking to the highly multi-core CPU roadmaps announced by Intel and AMD, that reduces even further the talent-pool:
<ul>
<li>Frontend: JRuby on a JVM, with Merb</li>
<li>Application Logic: Erlang. Actually, I'd love to see a Scala-like language targeted to the Erlang VM to make it more palatable. But for now, I'd settle on Erlang.</li>
<li>Persistence (non-relational): Erlang</li>
<li>Batch: Erlang </li>
</ul>
</li>
</ul>
