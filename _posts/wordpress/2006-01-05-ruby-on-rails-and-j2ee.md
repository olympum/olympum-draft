---
layout: post
title: Ruby on Rails and J2EE
date: 2006-01-05 16:40:00.000000000 +00:00
categories:
- Frameworks
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409306931826690'
  _edit_last: '1'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415065122;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:36;}i:1;a:1:{s:2:"id";i:45;}i:2;a:1:{s:2:"id";i:18;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I have spent some time over Christmas period playing here and there with <a href="http://www.rubyonrails.com/">Ruby on Rails</a> and getting an overdose of AJAX. I really wanted to see whether all the hype and marketing from <a href="http://www.37things.com/">37things.com</a> and associates makes any sense.

<p>I have two objectives in mind:</p>
<ol>
<li>Should I throw away J2EE for Rails?</li>
<li>Should I throw away PHP for Rails?</li>
</ol>
<p>My impression of Rails has been extremely good so far. However, I am really more pleased with Ruby than I am with Rails itself. Rails is interesting, don't get me wrong, but far from being revolutionary. All concepts and patterns in Rails have existed for a while in the Java and J2EE world for a while now. If so, why is Rails so cool and sexy? I'll give you a few reasons I found for myself:</p>
<ul>
<li>Ruby is a very expressive language for those like us coming from strongly typed language background.</li>
<li>Rails makes agile development easy. It is extremely easy to come up with a concept in the morning, and have a prototype in the afternoon to show to your client. This is because development and execution architectures are tightly coupled.</li>
<li>Rails principle of convention over configuration works great for 99% of the cases. No need to know how to define or configure something - it just works as long as you follow the principles.</li>
<li>Rails provides a really easy-to-use and lightweight structured MVC architecture for those PHP addicts hacking web site after web site.</li>
</ul>
<p>Would I throw J2EE away now that I encountered Rails? No. J2EE is a distributed component on steroids - so if you don't need distributed components, you don't need J2EE. But if you rely on JMS, JCA, JTA and distributed components, then Rails is not your medicine. Rails is a pure web application framework, with some quick O/R mapping facilities to ease the pain of DB access -- it's great for those web applications only backed by one database custom developed for the particular application. Rails is more of a pain relief for PHP folks than for Java programmers.</p>
<p><span style="font-style: italic">If you have been doing pure web frontends in Java using JSP and JDBC, well, sorry, I think you should go back and examine Python (Django), Ruby (Rails) and PHP (Yellow Duck, BlueShoes) and stop wasting your time.</span></p>
<p>Then there is <a href="https://trails.dev.java.net/">Trails</a>, a Java replica of Rails, using the "best-of-breed" Tapestry-Spring-Hibernate (yeah, fits my resume). However, I feel there is no much meaning in Trails nor TRAX. If I have complex problems (integration, distribution, transaction management, and messaging), I'll use Spring or directly the J2EE APIs, and will not rely on a generation framework and convention. I will want configuration, and full control.</p>
<p>Finally, there is also  <a href="http://www.phpontrax.com/">PHP On TRAX</a>, a Rails version for PHP. It might have a niche market, for those loyal to PHP. But given Ruby is sooo expressive, why would anybody program in PHP?</p>
<p>Bottom line, Rails and J2EE cover different needs and developer populations. There will surely always be an overlap - and over time they will both mutate to copy features from each other. But it is more likely that we see Ruby 2.0 running on the JVM, than iBatis or Hibernate on Rails!</p>
