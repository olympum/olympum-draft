---
layout: post
title: Will XMPP be the messaging middleware for the REST Web?
date: 2008-12-30 11:04:21.000000000 +00:00
categories:
- Future
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409187063201793'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415530188;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:254;}i:1;a:1:{s:2:"id";i:116;}i:2;a:1:{s:2:"id";i:129;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

We know the social web needs real-time event notifications, and that
polling sucks. Some are wondering whether we can implement it using
asynchronous messaging, ala Pub/Sub. The Publish/Subscribe is an
architectural paradigm allowing asynchronous messaging from one sender
(publisher) to many receivers (subscribers). PubSub is a common
architecture in financial services, since it's associated with
persistence and ensured message delivery. But such qualities don't
come for free: there are complexity trade-offs.

<p>Anyway, the conversation started in February, with Mickaël Rémond talking in his blog at ProcessOne (the maintainers of the top-notch Erlang ejbabberd XMPP server) about <a href="http://www.process-one.net/en/blogs/article/introducing_the_xmpp_application_server/">XMPP the application server</a>, where he turned the <a href="http://xmpp.org/extensions/xep-0060.html">PubSub XMPP extension</a> into a public event firehose for twitter. And because Mickaël puts his money where his mouth is, he opened a public service doing just that, <a href="http://www.process-one.net/en/blogs/article/tweetim_a_twitter_xmpp_gateway_service/">an XMPP gateway to twitter</a>, or what twitter should have done to begin with.</p>
<p>Then came Internet veteran <a href="http://one.valeski.org">Jud</a>, from upcoming <a href="http://gnipcentral.com">Gnip</a>, blogging about <a href="http://one.valeski.org/2008/06/sockets-http-xmpp-and-leap-frog.html">sockets, HTTP and XMPP</a>, and how the in the original non-reliable Internet topology the stateless HTTP worked because it brought reliability, but that today's reliable Internet topology could allow HTTP to be replaced by the stateful XMPP protocol.</p>
<p>It hit us again, at OSCON 2008 in July, with fellow Yahoo's hackers <a href="http://anarchogeek.com/">Rabble</a> and <a href="http://laughingmeme.org/">Kellan</a> talking about <a href="http://en.oreilly.com/oscon2008/public/schedule/detail/4359">data services streaming using XMPP PubSub</a>. We know that having to do frequent HTTP polling sucks, and unfortunately that's the best we can do many times, so they proposed to use a cut-down XMPP server (no roster, etc.) to build a public Publish/Subscribe messaging infrastructure. They worked it out for FireEagle and Flickr building external <a href="http://xmpp.org/extensions/xep-0114.html">XMPP components</a>, and connected a web stack through queues. XSF has gone further, proposing a new standard for <a href="http://xmpp.org/extensions/xep-0253.html">chaining components</a>, and why not, even <a href="http://xmpp.org/internet-drafts/draft-saintandre-atompub-notify-07.txt">a pubsub data stream for Atom</a>.</p>
<p>Honestly, there is plenty of buzz. Brian Dainton also talked about <a href="http://www.slideshare.net/bdainton/a-change-in-protocol-exploring-xmpp-in-ruby-presentation?type=document">XMPP for event broadcasting instead of REST</a>. The folks at <a href="http://www.chesspark.com/">ChessPark</a>, with <a href="http://metajack.im/about/">Jack Moffitt</a>, are doing just that with <a href="http://metajack.im/2008/08/04/thoughts-on-scalable-xmpp-bots/">component bots</a>.</p>
<p>It might be that XMPP eventually replaces HTTP for event notification, avoiding the need to poll. But today, HTTP and REST are patterns known to work. Let me examine why I think a REST approach still works better today:</p>
<ul>
<li>The Internet, the firewalls, the monitoring, are not built today for persistent connections. XMPP real-time events are possible since a TCP socket is kept open. <a href="http://xmpp.org/extensions/xep-0124.html">BOSH</a> and <a href="http://xmpp.org/extensions/xep-0206.html">XMPP over BOSH</a> make it possible to run XMPP over HTTP, and provide almost real-time notification. I like BOSH, a lot, but it is still an emerging technology that needs plenty of love. XMPP metadata is still not implemented in BOSH, and the client-side implementations are weak.</li>
<li>Running an Apache server and setting a up a REST service is almost straight forward. We know how it works, how it scales, and how it fails. Running a XMPP server, even the excellent ejabberd, is not as easy as running Apache, and most folks are likely not to run their own XMPP server and rely on third parties like jabber.org or gtalk. The good folks at <a href="http://blog.gnipcentral.com/2008/11/03/winding-down-xmpp-for-now/">gnip cut down on XMPP</a> because of lack of reliability of the XMPP third parties. XMPP, still, is too complex to operate.</li>
<li>Supporting <a href="http://metajack.wordpress.com/2008/06/10/binary-data-is-xmpps-achilles-heel/">binary data is XMPP's achilles heel</a>.</li>
<li>There are simpler HTTP only alternatives. <a href="http://brad.livejournal.com/2143713.html">Brad Fitzpatrick</a> implemented a never-ending Atom feed for the <a href="http://updates.sixapart.com/">LiveJournal update stream</a> years ago. A partial solution to reduce polling, although not real-time, is <a href="http://roy.gbiv.com/untangled/2008/paper-tigers-and-hidden-dragons">Roy's better resource mapping</a>. And let's not forget the straight forward <a href="http://joshua.schachter.org/2008/07/beyond-rest.html">callback</a>. Oh yes, <a href="http://mymobilesite.net/">running an Apache server on your mobile phone is possible</a>.</li>
</ul>
<p>Will XMPP become the messaging middleware for the web? Eventually, perhaps, but in today's environment, neither the infrastructure or the software are ready to support such a model. As importantly, there are simpler alternatives to achieve real-time event notification without requiring the publish/subscribe architecture.</p>
