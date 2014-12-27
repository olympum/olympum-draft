---
layout: post
title: Why Video-On-Demand Streaming in Airlines Sucks
date: 2008-08-19 01:59:11.000000000 +01:00
categories:
- Other
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409168054231041'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

It's rare to take a flight from British Airways or Virgin Atlantic
where the Video-On-Demand system just works. It might be a problem
only with UK airlines, but I presume this is a general issue across
aviation.

Sometimes you are part of the folks in the plane for whom the system
does not work. The crew will normally start rebooting your seat, then
the section, and then the whole plane. I guess they do so in hopes
that the operating system running the streaming adheres to the same
random rules as the one running on their desktop.

<p>In case of an incident with the entertainment system, i.e. in every single flight, the crew keeps apologizing about not being able to fix the problem and continue performing reboots left and right. Reboots are seldom able to address the problem, and the only thing reboots achieve is general frustration, both from those without video, but mostly from those with video who see their programs shut down. Eventually, the crew settles down to multicasting a few movies.</p>
<p>Virgin Atlantic even has the courage to advertise Virgin Media Broadband and TV packages on a commercial playing before the movie. Enjoy this cool entertainment system (that does not work) at home just like you do in the plane. I am no marketing guru, but that sounds to me like a dumb ass campaign.</p>
<p>I've seen a few times a linux boot-up sequence on Virgin, and I'd be surprised if BA was not also using Linux. Most likely, they are both using VideoLAN against one or multiple streaming servers with network attached storage. For whatever reason, it's the connectivity that fails, and the individual Linux workstations that fail to connect to the streaming server, or for the streaming server to be able to read the files from storage.</p>
<p>The reason to use attached storage is two-fold: cheaper, reliable and easier to update. But, guess what, wired networks don't seem to be reliable on a plane (probably because of the high-frequency power lines). So here's my advice folks: avoid the network (single point of failure). Here's how.</p>
<p>Virgin Atlantic has around 100 movies on inventory, plus TV series, CDs and radio programs. I'd bet their total inventory at any given point in time is between 250Gb and 500Gb. Maybe the solution to use shared storage made sense years ago cost-wise, but today the cost per Gb has fallen so much that internal disk storage could make more sense. Specially since there are no availability requirements (if it fails, a simple swap fixes the issue).</p>
<p>They could get a 1Tb disk per seat and image (push on the ground) all disks with the OS, the video player plus and the full media library. Re-imaging will take a few hours, but the inventory only gets fully updated every 2 to 3 months. Every seat would become an autonomous and reliable processing unit with its own storage. And in case of failure, it would only cost $100 to swap disk and reboot one seat, something the crew could do in-flight. No apologies, no pissed off customers, no compensation.</p>
<p>So, guys, go and implement it, so that I don't have to watch the beginning of The Oxford Murders from Alex de la Iglesia three times on my next flight.</p>
