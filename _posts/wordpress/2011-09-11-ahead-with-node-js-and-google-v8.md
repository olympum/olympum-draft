---
layout: post
title: Ahead with Node.JS and Google V8
date: 2011-09-11 15:34:12.000000000 +01:00
categories:
- Architecture
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409136882184194'
  _wpcom_is_markdown: '1'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

It has been 10 months since I posted about Google V8. But somebody re-started
<a href="http://news.ycombinator.com/item?id=2982684">a thread again on Hacker News</a>
about <a href="http://www.olympum.com/future/answering-jason-on-v8-governance-and-impact-to-nodejs/">my old blog
post</a>.
So now I am compelled to briefly say where we are at.

We have continued and extended our investment in Node.JS. I can tell you that
what the teams are doing is transformative and pure awesomeness. Unfortunately
this is as much as I can tell you right now, but really soon you'll start
hearing what we've done. In every single demo, internal and external, we have
done of the technology, the feedback has been fantastic. I am very happy and
fortunate to have a team of super-stars working on this.

As per my concern on being locked into Google V8 and not being able to support
the software, things have changed since I last blogged. First, Google has been
very, very, supportive addressing V8 bugs whenever they existed.

Secondly, here at Yahoo! we donated some code to the fine folks at Mozilla to
<a href="https://github.com/bfrancojr/v8monkey">wrap the Spidermonkey API with the V8
API</a>. Mozilla went on to create a full
implementation of <a href="http://blog.zpao.com/post/4620873765/about-that-hybrid-v8monkey-engine">Node.JS on
Spidermonkay</a>
and provide the architectural re-assurance we needed. I am still surprised
however from the discussion on the blogosphere and twitterspace months ago
about how many developers don't seem to pay attention to open source
governance. When you have the responsibility for a multi-million dollar
technology investment, you want to make sure you cover all your bases.

Finally, we have partnered closely with the fine folks at Joyent and are
working through the final stages of negotiation for how we'll work together
going forward.

Let me say that I am really excited about what the technology innovation that
Node.JS is bringing to the industry, whether that is to create a new
generation of I/O intensive servers, or to bring Javascript to the
server-side. I see Node.JS' future is bright.
