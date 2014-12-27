---
layout: post
title: Painfully HTTP Java
date: 2009-02-11 21:03:47.000000000 +00:00
categories:
- Java
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409168054231041'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I have been working on AtomPub and coding a prototype over the past
few evenings to get <a href="http://abdera.apache.org/">Apache
Abdera</a> talking to <a
href="http://couchdb.apache.org/">CouchDB</a>. I know there is an
experimental adapter in Abdera for CouchDB, but it does not use
CouchDB the way I need to.

<p>I decided to write my own provider, workspace manager, adapter, etc. I have been using <a href="http://code.google.com/p/couchdb4j/">couchdb4j</a>, the Java library binding used to talk to CouchDB, and <a href="http://json-lib.sourceforge.net/">json-lib</a>, a JSON library for Java.</p>
<p>Why, it has been <em>really especially extremely very</em> painful!</p>
<p>HTTP and JSON, REST a bit, and to a lesser degree XML, are supposed to be technologies that make your life easier as a programmer and as a server. But with Java, it's the other way round. What should be easy, becomes complex. I am very disillusioned about the suitability for the Java language in pretty much any domain related to HTTP.</p>
<p>With Java in HTTP, you have to jump API hurdles, pull hundreds of dependencies, and end up with stack traces deep as a black hole. Yeah, it works, mostly because of the amazing development support and tools for Java, such as Maven and Eclipse. But that alone does not make Java a viable technology for programming HTTP.</p>
<p>Java has it uses, and it is a good programming language. I don't think I'd ever code C++ again if I could use Java. But that's more on the number crunching, for the <a href="http://hadoop.apache.org/core/">Hadoop</a> of this world.</p>
<p>I'll stay with my PHP, Ruby and Python while I can. Perhaps it's also time to learn a functional programming language like Erlang.</p>
