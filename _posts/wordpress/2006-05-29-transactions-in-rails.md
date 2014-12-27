---
layout: post
title: Transactions in Rails
date: 2006-05-29 14:18:00.000000000 +01:00
categories:
- Frameworks
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409302838599680'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415377034;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:18;}i:1;a:1:{s:2:"id";i:15;}i:2;a:1:{s:2:"id";i:16;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

Transactions in Rails are starting to bother me, and quite a lot. Once in a while I dive into my latest application,booki.es, a web application for trading long-term futures using play money.

<p>Rails was fantastic for building my wife's eCommerce site: fairly static content and not many associations between entities. Rails transactional block was sufficient, something of the sorts of:</p>
<p>Account.transaction do<br />
account1.deposit(100)<br />
account2.withdraw(100)<br />
end</p>
<p>or</p>
<p>Account.transaction(peter, paul) do<br />
paul.deposit(350)<br />
peter.withdraw(350)<br />
end</p>
<p>Even ActiveRecord takes care of the transaction integrity for parent-child relationships, so when you save the parent, all child rows get also saved.</p>
<p>Now when a trade is exectued in my trading application, an update and a few reads happen on quite a few tables, including trades, positions, accounts, and historics, but some of these entities don't have any relationships between them. I need to ensure data integrity and atomicity, and Rails does not seem to have anything like the Java Transaction API (JTA).</p>
<p>I would love a simple transaction API like JTA being exposed for databases, like there is Transaction::Simple, but for databases.  Ideally, I would like to have nested transactional support, even if it is a flatten model like in JTS.</p>
<p>But I don't have it, so I am having to modify my controllers and models to overcome the limitation. And to be honest this sucks. Maybe I should go back to my Tapestry/Spring/Hibernate combo for this one app. The right tool for the right job ...</p>
