---
layout: post
title: Make your code obvious, or remove it
date: 2007-08-06 13:41:21.000000000 +01:00
categories:
- Architecture
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409249239584770'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

We have recently moved into a new house. The house is pre-wired with all sort of things one can imagine, for sound, video, network, motion, alarms, etc. It's really cool! But guess what, all wiring is behind plasterboards, and we don't have any instructions as of what and where it is. One end of all wires end up in one of the rooms, so I could put a high frequency pulse generator and trace down the wires behind the drywall. Sorted.

<p>Well, not really.</p>
<p>You see, whoever put that wiring in while the house was being built had an idea in mind. The wiring would fit into a particular set of sensors, alarms, and speakers. The builder was also conditioned by what was available in the market, so it planned wiring suitably for a multi-room A/V controller. The thing is, the builder left it "pre-wired", never finished it. Sort of an optional thing you could do whenever you moved in.</p>
<p>7 years later. Multi-room A/V and control systems have evolved so much that the technology the builder had in mind has been rendered obsolete.  1Gbit network now allows video streaming over CAT5e/CAT6 cables. So you don't need anymore expensive multi-room controller. I just need good network around the house, and commodity amplifiers in each room where you need sound/image/alarm, etc.</p>
<p>You see, all that wiring the builder put in? Useless.</p>
<p>Moral for us software engineers. Whenever you write a piece of code or implement a new feature always remember to make it obvious. And the best way to make it obvious is to make sure it is used. Don't write software for the just-in-case scenario.</p>
<p>You see documentation is good, very good, but there is no point documenting a feature that is not obvious. By the time you get to use actually it, it will be obsolete and too complex to make it worth understanding it.</p>
<p>In summary, it will always be easier to find out how things work, than how things could work. Things that work are self-explanatory: they are obvious.</p>
