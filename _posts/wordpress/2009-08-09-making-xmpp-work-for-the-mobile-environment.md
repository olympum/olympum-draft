---
layout: post
title: Making XMPP Work for the Mobile Environment
date: 2009-08-09 09:06:29.000000000 +01:00
categories:
- IMPS
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409166876033024'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415350646;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:97;}i:1;a:1:{s:2:"id";i:116;}i:2;a:1:{s:2:"id";i:79;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I've been thinking about a standards-based client for a mobile
environment. XMPP has quite a few strong merits, against it's
competitors such as OMA IMPS and SIP Messaging. For one, it's a
community standard, and it's actually possible to submit new specs if
so required. Secondly, it's becoming the standard protocol for IM, and
it's emergent in the open Pub/Sub infrastructure, i.e.
why-polling-is-bad.

<p>Unfortunately, there are still a couple of key problems with XMPP in a mobile environment - none of them can be solved in a standard way. I wonder if we could harvest a couple of good ideas from OMA IMPS and spec them under XMPP.</p>
<h3>Bandwidth</h3>
<p>The XMPP stream is verbose, which is not a bad thing by itself, except when you live in a mobile environment. Compression, either at the application (gzip) or the payload level (XEP-138), shifts the problem onto CPU cycles: you still need to decompress first, then decode, which increase latency and shortens battery life. Ideally, you would like to compress the payload onto something that can be decoded and parsed at once without requiring decompression, i.e. WBXML.</p>
<p>Unfortunately it seems like the community has previously slashed against these changes. When Google shifted from XMPP to its custom binary XML protocol for GTalk API, there was a heated discussion about its suitability. But what are folks suggesting that works for the mobile environment, and not just smartphones? I have not seen anything that would work in all phones, hence why WBXML. Please prove me wrong.</p>
<h3>Real-time Notifications</h3>
<p>The default XMPP stream uses bi-directional TCP/IP connections to allow real-time notifications (messaging, presence, etc.). Open sockets in a mobile environment are a bad idea for quite a few reasons, and although BOSH/HTTP-binding for XMPP solves the TCP/IP persistent connection problem, it is still expensive from a device perspective, as there is always a hanging HTTP request. As far as I can tell, there is currently no XMPP solution to this, and I can see how a extension to XMPP adding WAP-PUSH, WAP-UDP, and perhaps standalone UPD, would make sense.</p>
<p>Again, I'd like to think there is a standard solution for this. And no, iPhone Push notification does not really count.</p>
<h3>The Standard Way</h3>
<p>We can let folks come up with their own implementations, and then try to refit a spec for the sake of interoperability. But we know how difficult this becomes in other processes like Oasis, JCP, etc. I wonder then, if it is time now to spec this out, (and no, <a href="http://xmpp.org/extensions/xep-0239.html">spec jokes</a>, don't count):</p>
<ul>
<li>Binary XMPP</li>
<li>Push Notifications</li>
</ul>
