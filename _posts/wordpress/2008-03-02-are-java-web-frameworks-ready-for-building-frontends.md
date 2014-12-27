---
layout: post
title: Are Java web frameworks ready for building frontends?
date: 2008-03-02 21:02:31.000000000 +00:00
categories:
- Frameworks
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409204473364481'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415077341;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:16;}i:1;a:1:{s:2:"id";i:36;}i:2;a:1:{s:2:"id";i:10;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

Once every year I like to spend some time revisiting a personal itch
of mine: is Java ready for web prime-time? Sadly, although Java has
clearly proven its place in the server-side, it has failed in the
frontend, last bit of the server-side, the thin layer that transforms
business data into rendered HTML. This is what Rasmus Lerdorf calls
the "glue" (<a
href="http://www.php.net/manual/en/faq.installation.php#faq.installation.apache2"
title="PHP is the glue">PHP is the glue</a>), basically a thin layer
of presentational representation that links your server pre-assembled
data.

<p>Of course you could build web applications using either JSPs or one of the hundreds of web application frameworks available for Java. And a lot of leading players are doing just this. But contrary to some "enterprise" thinking, Java is by no stretch of imagination the leading language for web development.</p>
<p>The number of available web frameworks for Java is an indication of a ground where a problem exists that has not been addressed in any fully satisfactory way, yet. And I believe the key problem is productivity: Java is, still, not a productive platform for development, whereas it is probably the best available platform for production. And the thing is that although there is a very large, mature and globally distributed pool of Java server-side developers, Java is still hard to develop for because it is not a productive platform for this "glue".</p>
<p>A clue as of why it is not productive comes from analyzing the prime language users: the frontened web developers. It is actually really hard to find frontend web developers that want to use JSPs or any Java web framework. They rather use PHP, or Python, or Ruby, or Perl.</p>
<p>What all the P- scripting languages share in common is the low specs required to get started, the easiness itself to get started and hack something together, and most importantly that it only takes a single browser refresh to check any change and push the change to a production server. Sure, this is not a good practice (pushing to production), but it's something that for 99% of sites out there, it just works and it's good enough.</p>
<p>Java makes deployment hard. Starting a JVM takes seconds, refreshing a JSP takes seconds, changing classpaths, etc. require a restart or reload. Hardly productive. And the thing is, even though Java is more robust, better structured, and enforces better development practices, 99% of the sites out there just don't need this level of "enterprise" features. And I am not the only one saying so. Even Billy Newport, one of the lead architects behind WebSphere Application Server, and the Chief Architect behind WebSphere XD, has expressed this very same thought, that <a href="http://weblogs.java.net/blog/bnewport/archive/2006/06/java_versus_php.html" title="Billy Newport on PHP">Java needs to figure out how to become as productive as PHP</a>.</p>
<p>The productivity derived from the scripting language in those 99% of web sites out there is what makes Java unpopular for the remaining 1%. Java has to grow up in the web dev area. Ideally, one would like to take the best of both worlds: the robustness and performance of a JVM, and the productivity of the P-languages.</p>
<p>In my yearly review of the state-of-the-art, I am starting to think that this change to make Java more productive is finally starting to happen in 2008. First was the advent last year of the scripting languages becoming a target of the JVM, such as Jython, JRuby, PHP, Groovy, Scala, etc. made it possible to benefit from the JVM robustness. But still one had to suffer the JVM weight inflicted by Java (the language) centric development practices.</p>
<p>It's really only been over the last 6 months when we have seen a number of open source and closed-source projects taking on the task of bridging the scripting and JVM world together for web development. A couple of the web frameworks that I am interested in researching more about and that look rather promising to me are <a href="http://www.projectzero.org/" title="Project Zero">Project Zero</a>, and <a href="http://code.google.com/p/liftweb/" title="Lift web framework">liftweb</a>.</p>
<p>In summary, I really think we may be looking at 2008 as the year when Java finally graduated in the web dev frontend area. I certainly hope so. But only time will really tell.</p>
<p><span style="font-style: italic" class="Apple-style-span">Disclaimer: this is not, by any stretch of imagination, Yahoo!'s official view. Don't try to read too much into this posting. For those that know me well enough, you'll know that I have been looking into application frameworks, web and others, since 2000.</span></p>
