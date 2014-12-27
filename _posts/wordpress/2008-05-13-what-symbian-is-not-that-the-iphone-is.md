---
layout: post
title: what the iPhone is that Symbian isn't
date: 2008-05-13 09:52:25.000000000 +01:00
categories:
- Mobile
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409168054231041'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415228454;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:67;}i:1;a:1:{s:2:"id";i:279;}i:2;a:1:{s:2:"id";i:55;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

one of the key strategic questions that developers looking into
creating successful mobile applications need to answer is the choice
of platform. we see an increasing consumer demand for desktop-like
rich applications on the phone, but somehow the promise of such
applications remains undelivered. developers can chose between the
smartphone centric OSes, Windows CE and Symbian, or the desktop
centric OSes, Linux and OS X. so which one should we chose to build
those future desktop-like applications?

<p>smartphone centric OSes are designed to address the limitations of the constrained mobile environment, while at the same time delivering a rich user experience. typical constraints range from input methods, battery and connectivity. let's be clear, these are good phone OSe,s, and they make good phones. but interestingly, these are constraints that have started to go away, and are becoming largely irrelevant, if not already irrelevant.</p>
<p>mobile network connectivity now offers full TCP/IP stacks on always-connected phones under flat fee transfer rates. battery life on most new phones allows such stack to be always on without significantly affecting the batter life, and input devices such as the iPhone demonstrate that the paradigm can be changed for the best.</p>
<p>in contrast, desktop centric mobile OSes are not really designed for mobile environments, and mobile is just an add-on. where the smartphone centric OSes need to impose API limitations, the desktop centric OSes don't impose almost any. where the smartphone centric OSes excel as phones, the desktop centric OSes tend to lack important features (the iPhone is a good computer but a really bad phone).</p>
<p>and the question really for developers starting now a new application is whether to develop for such phone-focused OSes, given the large market share, and hoping that they will be enhanced sometime in the future to become full OSes, or whether to go for desktop centric OSes, with currently a smaller market share, and hoping that the mobile features on the them are sufficient. in other words, what's more likely to happen, a desktop centric mobile OS being enhanced to become better phones, or a smartphone centric OS being enhanced to become a better desktop?</p>
<p>the answer to this leaves within the OSes themselves. today, the iPhone is an excellent mobile computer based on the OS X, but it's a really bad phone. however, the mach/bsd kernel, the quartz framework and the cocoa framework should make it relatively easy to add GPRS and UMTS to an iPhone. and possibly the only reason it's not there is purely commercial, based on the current distribution deal with AT&amp;T.</p>
<p>in contrast, you can't make a good desktop OS out of the smartphone centric OSes. they are simply crippled. i find it surprising to see how analysts overrate the symbian os. technically, symbian is a really unattractive and unproductive development platform to work with. commercially, it's a fragmented market with three competing and somehow incompatible platform variants: nokia's s60, sony-ericsson's uiq, and ntt docomo's moap.</p>
<p>from a technical standpoint, symbian has its own memory management and exception handling mechanisms which lead to a crippled and unfriendly C++-ish variant. symbian support for string handling is as bad as it gets, and even php does a better job! finally, writing complex interaction paradigms and network access is daunting: multi-threaded applications for symbian requires rocket scientists. and finally, and most importantly, the development environment is simply non-existent, mostly because of the custom C++ memory management and complex deployment process.</p>
<p>very sadly, java does not make a much better symbian. although language and tool support is excellent, the lack of uniformity on the platform itself, with MIDP 1.0 and 2.0, being implemented to different degrees by different vendors and by models, has resulted in tens of different APIs supported by some but not all phone models. it's really hard and time-consuming to develop for java applications for symbian. either you create multiple variants of your application, or you cut down to the least common denominator. neither option is attractive from a developer standpoint.</p>
<p>windows ce suffers similar problems to symbian. the programming model is overly complex and based on the highly developer unfriendly win32 api. alike java, the .net compact framework has not been consistently adapted, so one ends up with multiple binary targets, that require separate code, debugging, testing, distribution and installation. a nightmare from a developer's perspective. on the plus side, windows ce development environment is superb, including remote debugging abilities on the device itself. but overall, i discount windows ce as a no-go platform.</p>
<p>this really cuts it down to desktop centric OSes being a better choice for development going forward. that's really between OS X and Linux. and i am picking OS X and the iPhone. here's why.</p>
<p>as with anything linux, mobile linux is really many many things. different vendors have implemented things differently and are providing different stacks. some offer Qtopia, from Trolltech, some offer Gnome. then you have android, openzaurus, openmoko, ... no one phone has a significant market penetration, and to develop for linux really requires multiple binary targets and API abstraction layers. again, it's making things more complex than it ought to be.</p>
<p>in terms of kernel and integrated development environment, OS X is a much better platform. it's a highly productive environment. but it's proprietary to apple. which is good and bad. it's good since you know what hardware and software you need to support. it's bad since you are locked in, including for distribution.</p>
<p>but here comes the twist. developing a cocoa-based application for the iPhone is extremely easy, and given that Linux and OS X (mach/BSD) share so much in common, moving an iPhone application to a linux variant would not be any harder than moving between Gnome and Qt. good OO design should make it relatively easy.</p>
<p>in summary, iPhones features a robust and rich OS, OS X, a highly productive development environment, an aggressive market share growth, and lots of similarities with Linux. these are all good reasons to me to pick the iPhone as the target mobile platform of the future. i am not fully discounting linux however. the current issues with lack of significant market penetration could be overturn, specially in asia, and particularly in china.</p>
