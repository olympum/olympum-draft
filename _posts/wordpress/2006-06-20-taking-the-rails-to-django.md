---
layout: post
title: Taking the Rails to Django
date: 2006-06-20 21:08:00.000000000 +01:00
categories:
- Frameworks
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409291324833792'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

While developing our trading application, I have come across two key things Rails does not have.

* Transactions. Rails does not offer distributed transaction management. This does not bother me much, since I am not a fan of having transactions span across multiple datasources. However, Rails does not offer cross entity transaction management on a single datasource for unrelated entities. The Rails model works well for ensuring autocommits on parent-child relationships, but anything beyond that requires extensive work and bookeeping in your controllers. For most jobs, the Rails model is enough, and does the job. It actually does the job pretty well. But there are jobs, such as updating multiple trading and position tables where Rails is not the right tool.
* Security. Rails is absolutely agnostic of security. Authentication, authorisation and Access-Control Lists are foreign to the framework, by design. The whole plumbing required may become daunting, and while there are engines and plugins out there doing part of the job, I truly hate taking ownership for the security bits within my application.

_Localisation and internationalisation is yet another third a bit weak in Rails, but I  am yet to have true requirements in this area to be able to give an opinion._

Anyway, Django looks like a promising alternative. It offers both more comprehensive transaction management support and a complete security model, with the whole plumbing being in the framework itself. Whether it will fit the shoe, we'll see as soon as I write the order island book.
