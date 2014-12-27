---
layout: post
title: Java EE 5, still too complex
date: 2006-06-12 10:52:00.000000000 +01:00
categories:
- Java
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409296311869440'
  _edit_last: '1'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

The Java EE 5 architecture, with its use of annotations brings the Java world <span style="font-style: italic">close</span> to being agile. The architecture is absolutely fantastic and powerful, with superb messaging (JMS), persistence (EJB3), transactions (JTA), and integration (JCA) capabilities.

<p>However, on the presentation side, for the web world, Java is still behind both .NET and agile frameworks like Rails or Django. JSF is cumbersome, and still too attached to the systems-programming intensive request-response Model2 that ended up in JSPs and Struts. Wicket and Tapestry are possibly the top component-based development web frameworks for Java. But they are both only used by a relatively small community, and documentation, mostly in the case of Wicket, is deficient, especially when it comes to topics such as integration with persistence frameworks.</p>
<p>In terms of setting a complete development environment, it is painful. Setting up Netbeans/Eclipse, JBoss/Geronimo/Glassfish, Wicket, and EJB3 to play nicely with each other is not easy, and it has lots of rough edges. It takes too long to setup an environment and start coding.</p>
<p>That myriad of frameworks and standards is what makes Java EE so powerful, yet so cumbersome. I was hoping annotations could have solved most of the integration complexity, but I am disappointed. So, sadly, my hopes for a "new Java" are yet once again down. Java EE still gets on your way to being productive.</p>
<p>I am back to Rails for the time being, at least until Java EE 5 matures.</p>
