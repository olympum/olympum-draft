---
layout: post
title: SOA, can it scale?
date: 2006-01-09 16:23:00.000000000 +00:00
categories:
- Architecture
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409305409318912'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

SOA means a lot of different things to different people. Now, if I go by the W3C's definition, it's about processes that assemble services and an organisation that owns the processes and the services.

<p>However, to me, SOA is simply distributed computing over web services. I have been building distributed component applications since 2000 that were exposed as business processes. We did not have web services, but the facade was a process interface, and the execution was managed by a simple workflow engine. BPEL and SOAP were not yet mainstraim, still our application was based on a SOA.</p>
<p>So what makes a SOA different from good practice in doing distributed components (the service facade, service locator and state machine have been published design patterns for a while now). I think the only difference is the message encoding protocol (SOAP).</p>
<p>So, what's with SOA scaling?</p>
<p>Many organisations are adopting SOA as almost the holly grail that would enable them to achieve reuse. For a SOA to succeed, one needs to think about processes and data.</p>
<p>Organisations that start now modeling on the process side, and construct processes assembling services exposing existing legacy systems, will hit a big performance wall. You need to think about data: ensuring a given entity ownership sits in one or few known parties. Otherwise, each service part of a larger process will access records which are not necessary for the 'whole'. A little performance overhead summed up over a bunch of services that constitute a process results in possibly non acceptable overall service performance.</p>
<p>Those organisations that decide to focus on the data side encounter the reversed problem - you can't work in your information architecture if you don't know who is using you. So if you just build services and processes that expose existing data, you are doing it in a best-effort basis. It may, or may not, fit the interface and data needs of the service consumers. If they don't, they will need to go against your datasources directly, and this will defeat the whole reason for an SOA.</p>
<p>I believe the following development methodology for services could work:</p>
<ol>
<li>Model your processes, analyse the required data and use those requirements to create a data model.</li>
<li>Create a true component architecture, with proper entity relationships and ownership to encapsulate and abstract your data model.</li>
<li>Create services and assemble services according to your process design (which you may/should revisit by now).</li>
<li>Iterate the previous steps, starting from the core business processes, and adding processes to the SOA.</li>
</ol>
<p>Interesting enough, this is how agile web 2.0 development is happening! Start off with HTML screens, then model your DB, then construct your model, controller and revisit the views. Which brings me back to the web 2.0 == SOA. We'll eventually get there ...</p>
