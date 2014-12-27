---
layout: post
title: 'NodeJS: To V8 or not to V8'
date: 2011-02-06 00:05:01.000000000 +00:00
categories:
- Future
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409142041174018'
  _wpcom_is_markdown: '1'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415454461;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:335;}i:1;a:1:{s:2:"id";i:340;}i:2;a:1:{s:2:"id";i:347;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I have been saying for a while that <a
href="http://www.olympum.com/internet/why-node-js-matters/">server-side
Javascript matters</a>. We, at Yahoo!, see <a
href="http://developer.yahoo.com/blogs/ydn/posts/2010/11/on-deck-yuiconf-2010-with-a-focus-on-yui-yql-and-node-js/">a
bright future in server-side Javascript</a> and are making a big
investment in it. But if you <a
href="http://twitter.com/olympum">follow me on twitter</a>, you'll
know that I am also looking into ensuring high-availability of
server-side Javascript-based services on production. Which really
comes down to something like: to V8 or not to V8.

If you have not watched <a href="http://www.yuiblog.com/blog/2010/08/30/yui-theater-douglas-crockford-crockford-on-javascript-scene-6-loopage-52-min/">Douglas Crockford's video lecture on server-side
Javascript</a>,
I recommend you do that first before reading further into this post.

<strong>Update:</strong> Jason Hoffman (Chief Scientist, Founder of Joyent) has written a <a href="http://joyeur.com/2011/02/05/on-brunos-concern-about-the-current-coupling-of-node-js-and-v8/">very good response</a> to this post. Obviously I owe him some responses, which is <a href="http://www.olympum.com/future/answering-jason-on-v8-governance-and-impact-to-nodejs/">on a separate post</a>.

<p>NodeJS is currently tightly coupled to Google's V8 engine. V8 was not designed
as a server-side engine, but as a browser-based engine. Furthermore, V8 was
designed squarely to run in Chrome's multi-process model. As much as I think
V8 is a brilliant piece of engineering, it's software that was not designed to
run on a server.</p>
<p>More to the point, it's really up to Google to work with the community to make
V8 work on the server-side. Sometimes Google is responsive, but sometimes it
might not. It varies as it depends how fixing a bug or applying a patch may
align with Google's product roadmap and plans. I don't know Google's plans, and I
suspect most NodeJS committers don't know either.</p>
<p>Maybe for some folks this might not seem like a big problem. And probably, if
you are running a site with a few thousand daily page views, it might actually
not be a big deal. But to Yahoo!, and <a href="http://amix.dk/blog/post/19577">to
others</a>, it's a big deal and we believe this
is fundamental to the success of the NodeJS project.</p>
<p>Writing a Javascript runtime that does not fail is hard. Even the really smart
V8 folks have explicitly designed V8 for failures to happen and safeguard the
browser. In a browser, a JS engine failure is an inconvenience to the user:
damn, you lost a tab. In a thread-per-request blocking I/O server design it's
also not a big deal, you lose one in-flight request. But in an event-driven
web server, it's a major flaw, you lose thousands of in-flight requests you
have already accepted.</p>
<p>For NodeJS to scale to billions of page views like Yahoo!'s, we need to
make sure the Javascript engine / VM behind Node is rock-solid for server-side
loads, i.e. it fails extremely rarely.</p>
<p>Google may invest on supporting V8 on the server-side, just like the Mozilla
folks do. Or somebody else might invest and ensure V8 is rock-solid on the
server and Google may merge the patches nicely. Or maybe not, and the
community may need to fork V8. Or something else ... Nobody really knows.</p>
<p>Either way, it's time for the NodeJS community to realise there is a
roadblock and discuss it openly.</p>
