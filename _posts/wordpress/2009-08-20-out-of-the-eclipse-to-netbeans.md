---
layout: post
title: Out of the Eclipse to Netbeans
date: 2009-08-20 15:51:36.000000000 +01:00
categories:
- Java
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409167438065665'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415330843;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:354;}i:1;a:1:{s:2:"id";i:355;}i:2;a:1:{s:2:"id";i:10;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I have been using emacs and the command line for now almost 20 years. Once in a while, I dip into IDEs, but always go back to the command line. My biggest gripe with IDEs is that it keeps me away from the actual build, and that I normally have to spend time duplicating building configuration in the IDE. The canonical source for build configuration should be the build system (Make, ant, maven, etc.). With an IDE one would have to always be things in sync, leading to errors and all sort of weird stuff.

<p>But I keep trying looking for the holy grail. In the past, I've been relatively happy with Eclipse for the odd refactoring job. I would fire it up, fix, and close it, back again to the command line.</p>
<p>This time around, I wanted to see if an IDE would make me stop using emacs. I set myself a few requirements:</p>
<ul>
<li>Auto-complete. Not intellisense crap. Basic emacs completion is enough.</li>
<li>Maven is the source. I don't want to keep a parallel reality when maven poms have all the information already on it.</li>
<li>Unit testing. I want to run and debug my unit tests from the IDE.</li>
<li>Basic re-factoring, especially code usage reports.</li>
<li>Light on resource usage.</li>
</ul>
<p>I looked into IntelliJ IDEA 8.1, Netbeans 6.7 and Eclipse 3.5. Here are my findings.</p>
<h3>IDEA</h3>
<p>I got an evaluation license and only used it a few days. IDEA is a fantastic IDE, and despite high memory consumption, it felt light-weight and kept the system very responsive. In principle, it met all the requirements, and the refactoring support was simply the best out of the lot. However, at some point things started to go wrong:</p>
<ul>
<li>Compilation errors. Cannot find symbol, although running maven from the command line would not throw any errors. I did not want to spend figuring out what was wrong here. I am sure some IDEA expert would have told me I was doing something wrong, or that some configuration had to be changed. But IDEA was already failing the requirement: maven is the source. I don't want to fiddle around with the IDE settings.</li>
<li>Mercurial integration problems. The plugin kept on throwing up and breaking the environment. I had to uninstall it, but that's really a minor point.</li>
</ul>
<h3>Eclipse</h3>
<p>Then came Eclipse. Overall it looked good, but there was no Maven support out of the box. I tried installing Q4e, but getting JUnit support in debug mode was just too painful. m2eclipse worked fine, and Eclipse met all requirements with it.</p>
<h3>Netbeans</h3>
<p>Netbeans was last. I've never liked Netbeans. But I did now. A lot.</p>
<p>It looked good. It mapped nicely into OS X, which the others did not, in terms of user input and display. It supported Maven out of the box as a source of truth for build configuration. It offered substantial more refactoring features than Eclipse, but less than IDEA. Mercurial integration was spot on. And I could run my unit tests in debug mode.</p>
<p>But most importantly, Netbeans did not get on my way. I did not have to configure anything to get going. It was like using emacs, but with all the goodies.</p>
<h3>The winner</h3>
<p>I am going for Netbeans. IDEA looks good, but I am not sure I would pay out the license fee for the powerful refactoring features. Others might, but I probably won't. Eclipse was also improved, but having to fiddle with plugins to get Maven support was really sub-standard.</p>
<p>So, it is Netbeans.</p>
