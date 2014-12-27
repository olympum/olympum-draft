---
layout: post
title: 'Corporate Technologities: Keep the Power On!'
date: 2007-02-13 07:18:17.000000000 +00:00
categories:
- Architecture
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409269187289089'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

Any small startup that succeeds and grows to become a big corporation will suffer from technologitis, this is, the inflamation of technology and detachment from the business body.

<p>Seriously, the startup mode, where technology governance is not necessarily as important as time-to-market, allows for dynamic environments that allow quick growth. But at the cost of increasing operational costs due to technologitis: most of the IT budget being spent in operations, in keeping the power on, and only a little fraction of the budget is actually spent in new business initiatives. Certainly not the place the business would like to be in.</p>
<p>Over the last couple of years, a lot of folks have been switching their strategy in chip technology, going from Sun SPARC to Intel Xeon, IBM Power5 to AMD Opteron, Intel Xeon to SUN Niagara, and what else. The end result is that as much as they might have solved a point problem, on the long term they have increased their operational complexity.</p>
<p>There is nothing wrong in switching technology, but one must be aware of the technology cycles inherent with any technology. Whereas changing an application framework is something that theoretically one can do every 12 to 18 months, given that major version upgrades tend to be quite <em>dramatic</em> it would not be that much additional cost to ditch the framework altogether (but beware, project managers will tell you otherwise).</p>
<p>But CPUs stay in the data center for at least 3 years, mostly 5 years, and sometimes even 6 or 7 years. A choice of CPU technology should be long-lived (some may argue CPUs are a commodity, but once you start facing bugs traceable to specific architectures, you wonder whether you would not be better off standardising on a single architecture). A particular vendor may not have at all times over 5 years the fastest, coolest, higher bandwidth chip out there, but good vendors will come regularly come back to take the first place</p>
<p>Before the release of Sun Niagara, Sun failed (repeatedly) to meet its own objectives and bring out its Rock processor, up to the point that it cancelled the whole project. The PR impact was damaging, as well as the effect on the books, and the stock plummeted. After the release of Niagara, a lot of folks came back looking at Sun, hoping all trouble was over. The chip is good, but the question is not whether <em>is </em>good, but whether Sun is able to keep innovating over the next 10 years to ensure the chip <em>remains</em> good.</p>
<p>Apple was using the IBM PowerPC chip on their laptop, desktop and server product line. But IBM was focused on its own server business, and engineering the Power5+ chip. Apple needed a low power high clock device that would make the Apple truly competitive with Intel's and AMDs' offering, otherwise their laptop sales would never go higher than PCs. The switch to Intel is surely costing Apple a lot of money in development, marketing and lost opportunities (not all software is ready for Intel). This switch it has however also served as a good marketing effort to bring it on front of typical PC users, and the Intel chip is still faster and cooler than a PowerPC. But what is really important as a lesson is that Apple switched vendors, not technologies.</p>
<p><a href="http://www.theregister.co.uk/2007/02/13/ibm_power6_twice/">IBM just released yesterday a note on Power6</a>. Power6 chips will be coming up in mid-2007, at clocks reaching 5Ghz, with double the clock, double the bandwidth, and most importantly the same power profile. This is an amazing individual breakthrough, but nothing you would not expect out of one of the best research labs in the world, IBM's Almaden Research Center.</p>
<p>But while IBM keeps on delivering new technology breakthroughs, Sun has failed repeatedly in the past. Sun will have to prove itself repeatedly to stablish its credibility back. On the x86 side, AMD has shown historically its ability to innovate in the server space, and, to a lesser degree, Intel.</p>
<p>That's why for servers I will keep on recommending AMD/Opteron (Linux) and IBM/Power (AIX). They are cool, they keep your data center cool, and make you look cool! But whatever you happen to chose, make a good choice of vendor, not just technology, and stick to it for as long as the technology life is. Otherwise you will end up with technologitis.</p>
