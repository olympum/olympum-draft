---
layout: post
title: A week of KDE (killall evolution-data-server)
date: 2007-08-03 16:06:58.000000000 +01:00
categories:
- Linux
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409248635588609'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

See, I can live with Evolution crashing once in a while. Hell, it's software, it's <em>meant</em> to fail. But another thing is when the whole damn thing fails silently and in consequence kills your productivity. Evolution has  managed to randomly delete part of my calendars, appointments here and there, and multiple appointments moved in time. End result, missing meetings and looking like a complete idiot. The top of the iceberg happened on Monday when Evolution corrupted one of IMAP folders. Ouch! Pain, I know, I hear you.

<p>I am off Evolution. evolution-data-server is just waaaaaaaaay too buggy. Sometimes I wonder if Novell buying Ximian was actually such a good thing ... but anyway that's another story.</p>
<p>What I am using now? Shh, don't tell anyone! Kontact, KAnything, KThis, KThat, KSomethingElse ...  KDE!</p>
<p>Being a Mono/GNOME fanboy, I have set myself a challenge: only use KDE and stick to native KDE apps for a week. Well ... I <em>really</em> meant to stick to Konqueror, but after 10 min I had to give up on that - I had forgotten the web does not run on standards - or does it?.</p>
<p>For the good news, I am feeling (surprisingly) productive. KDE apps are extremely well integrated with each other. There is a continous flow of information, your data is easily shared. I actually feel good. Call it Productivity Pr0n.</p>
<p>One thing I am missing badly is something like Tomboy, the Gtk#/Mono personal Wiki. I am trying Basket instead, which happens to be tighly integrated into KOffice. Unfortunately I have not managed to get beagle to index basket notes. I actually tried strigi instead of beagle, but it failed to index 50% of my docs because they were not UTF-8 or latin1. Plus strigi had no stemming. Oh, and that it core dumped at 120k docs ... Guys, better fix that for KDE4!</p>
<p>The worse side of KDE so far is configuring anything K related - it is an authentic nightmare!  I know it's intentional, but, really, it's not my metaphore. I would be happier with  sane defaults and not seeing all those other 3 zillion configuration options. I love to have them, but hidden. On KDE's behalf, KDE actually let's you configure stuff that you just can't in Gnome (a good thing). The problem is that you need to be the developer to know which combination of options gets you what you want!</p>
<p>Anyway, I am quite happy so far. Some of the KDE apps, kick ass big time. And my calendar events are not silently flying off all around the place.</p>
<p>Oh, and remember:</p>
<p><code>$ evolution --force-shutdown</code></p>
