---
layout: post
title: Oops, Trying out Yahoo!'s OpenID V2
date: 2008-01-19 15:48:29.000000000 +00:00
categories:
- Yahoo!
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409217115004928'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I set myself to write last night a simple PHP OpenID consumer for
Yahoo's! However, I have encountered the Oops message that most folks
have also faced:

<blockquote><p>Ooops...<br />
Hey there! You have stopped by a bit sooner than we had expected. This feature is still being tested, so please check back later.</p></blockquote>
<p>Anyhow, I think it's really cool, both for users and for application providers, for a whole number of reasons:</p>
<ul>
<li>OpenID V2 has the notion of Directed Identity, which from a user's perspective simply means not having to know that you are using OpenID (like it should be). In other words, <strong>it just works</strong>. A simple HTTP POST to yahoo.com and you are all set!</li>
<li>There is no need anymore to go through hurdles of storing user information and mapping users, like you almost always had to do with OpenID. With OpenID V2 the consumer can query profile information from the OpenID provider. The user has the control to select from a number of profiles stored on the provider, and even pick what attributes in a given profile get shared with each consumer. <strong>The user is in control!</strong></li>
</ul>
<p>Really, this is really exciting, and makes me very proud of being a Yahoo! ;) I'll pick this test back once we go live by end of this month.</p>
