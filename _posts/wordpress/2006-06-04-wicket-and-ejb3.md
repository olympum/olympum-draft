---
layout: post
title: Wicket and EJB3
date: 2006-06-04 13:16:00.000000000 +01:00
categories:
- Frameworks
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409297431732224'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415214004;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:16;}i:1;a:1:{s:2:"id";i:10;}i:2;a:1:{s:2:"id";i:12;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I have tried for the last couple of days to overcome some of the transaction management problems I was having with Rails, and the more I look at it, the more I am convinced Rails is not right for my trading application. Rails has its sweet spot, and for me, there won't be anymore PHP.

<p>I came back to my usual Java stack, with the usual suspects, Tapestry, Spring and Hibernate. But, after the Rails experience, it was just ... yuck! The development environment is complex to setup, there are library dependencies, tons and tons of XML sit-ups! Enough!</p>
<p>I would like to use annotations, and it seems like Hibernate and Tapestry all have it in already, so no more need for XML files, and complex build and packaging using XDoclet. But development environment support for this flavour is very flaky. So much, that I got frustrated.</p>
<p>And this made me re-evaluate an old friend: EJBs. The EJB3 in JavaEE 5 leverage the annotations to make it expressive and put the focus on the model.</p>
<p>I have no more need for Spring, which I was only using for transaction management. I am happy with stateless EJBs.</p>
<p>I have no more need for accessing Hibernate directly. I rather using Entity Beans, and have the implementation be Hibernate3 (wow, I am sooo surprised to read this ... given how such of an anti-entity beans advocate I have been!!).</p>
<p>And as for Tapestry - well, sorry. It's just too much, even with Hivemind. Unit and integration testing is still hard with Tapestry, and there are far too many conventions around.</p>
<p>Which only left me JSF and Wicket on the web component development frameworks front. And given that I don't like the JSP baggage in JSP, I'll go for Wicket, which shares a lot of the Tapestry principles.</p>
<p>So, my new stack is Wicket 1.2 and EJB3. Let's see how it goes.</p>
