---
layout: post
title: Answering Jason on V8 governance and impact to NodeJS
date: 2011-02-06 05:30:44.000000000 +00:00
categories:
- Future
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409143316234240'
  _wpcom_is_markdown: '1'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415454509;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:330;}i:1;a:1:{s:2:"id";i:347;}i:2;a:1:{s:2:"id";i:315;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

Jason Hoffman (Chief Scientist, Founder at Joyent) has posted some <a
href="http://joyeur.com/2011/02/05/on-brunos-concern-about-the-current-coupling-of-node-js-and-v8/">good
questions to me</a>, based on my original <a
href="http://www.olympum.com/future/nodejs-to-v8-or-not-to-v8/">nodejs
and V8</a> post. Let me summarise Jason's questions and comments.

<strong>Update (2011/9/11)</strong>: this post is picking up again 8 months later, I've <a href="http://www.olympum.com/architecture/ahead-with-node-js-and-google-v8/">written an update</a> as of where we stand.

There are three key messages in Jason's response:

> It's Joyent's responsibility that NodeJS runs well period. We're not
> afraid of a language VM. [...] actual node.js committers (who all work
> at Joyent) know quite a bit and have pretty good relations with the V8
> team.

<p>That's a very honourable goal and perfectly within Joyent's capabilities and track record. I am <em>not</em> debating that.</p>
<blockquote><p>
  If there are actual technical problems with V8′s reliability or ???
  and these affect the use of node.js in production then I’d like to
  see details.
</p></blockquote>
<p>The discussion is not really whether I have technical production problems or
not with V8 (within NodeJS); all software has bugs. My issue is about project
governance. Let's say such a problem affecting reliability exists and that
Joyent fixes it by developing a critical patch for V8, a patch that the
upstream maintainer does not deem it necessary to merge. For how long would
Joyent maintain and test such patches?</p>
<p>Another aspect of governance: intellectual property rights.</p>
<p>My point: it's not whether Google's V8 project is open or not, it's that since
governance of V8 may become a problem <em>in the future</em>, it requires a solution
<em>now</em> so that large organisations can put their full weight behind NodeJS.
Joyent's weight behind NodeJS is necessary, but not sufficient. I prefer
addressing the problems in the code.</p>
<blockquote><p>
  node.js is only implemented on V8 but that’s only because we’re
  going to focus on making node.js awesome first. [...] After all, we
  are still working on getting it to 1.0
</p></blockquote>
<p>Open source software is commonly designed to make it easy to replace parts or
components that may be at risk of being legally tainted or patent encumbered
(e.g. mono's architecture as an example of isolation). I would put V8 in the
same bucket of "risky parts", although for different reasons. Given the lack
of definition on Google's V8 project governance, and the current tight
coupling between node and V8, I wonder how realistic it will be to implement a
different VM post-1.0 if we haven't got the right layer of abstraction
pre-1.0. Or perhaps the problem (the reassurance of governance) can be
addressed by working under the umbrella of a foundation that ensures such
governance.</p>
<p>Let me end by saying that I am still as committed as ever to NodeJS and that I
really believe in Joyent's engineering strength to make NodeJS 1.0 a reality.
Joyent is putting their money where their mouth is. We know they are working
hard making node <em>awesome</em>.</p>
