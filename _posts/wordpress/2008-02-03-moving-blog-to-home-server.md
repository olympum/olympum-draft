---
layout: post
title: Moving Blog to Home Server
date: 2008-02-03 19:44:50.000000000 +00:00
categories:
- Linux
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409211595694080'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I have been running this blog on a slicehost VPS with excellent
results so far. However, I am at the point where I need a bit more
flexibility and I can't justify the $20 monthly fee to my home CFO.
So, I did setup myself to move the server back home this weekend,
where funny enough, I used to host this blog.

<p>The first choice came down to choice of OS. I had been running Gentoo, but I have found this distribution bad for very low spec hardware. I am running on a fanless and rather exotic VIA C3 533Mhz chip, and compiling packages isn't particularly a fast thing on this box. I tried Gentoo a couple of years back on it, and getting gcc to compile would take a couple of days. Plus at some point it stopped working because of not sufficient memory.</p>
<p>Going through the choices I hesitated for a while with FreeBSD, but lack of good references for my CPU made me look at the Linux side, where I considered CentOS5, Debian and Ubuntu. I did not like CentOS RPMs - I don't any value-added on top of RHEL, and it feels odd to go free beer, but not free speech. That left Debian vs Ubuntu.</p>
<p>Whereas I have been relatively happy with Ubuntu as my laptop's OS for the last three years, I don't think Ubuntu has the necessary levels of testing required to "certify" a server OS. So I picked Debian, but instead of running stable (etch), I decided to go for test (lenny). Not as aggressive as Ubuntu, which is based on unstable (sid). Additionally, some packages I need (e.g. gmp for php) were not available in Etch.</p>
<p>So far, setting up the box to replicate the slicehost configuration has been relatively easy, with the exception of the MTA/IMAP which is always a pain. Have I had more memory and CPU I would have installed Zimbra. But since I am not sure my home CFO is going to be very impressed with me asking for yet another computer, I think I'll pass on Zimbra for now.</p>
<p>The initial install out of a bootable USB went without complications picking a basic setup, after which I added MySQL, Apache, PHP, Postfix and Cyrus. I prefer to add the stack by hand, to control exactly what gets installed. Finally, the upgrade to lenny was also extremely smooth.</p>
<p>I have now finished reconfiguring all DNS records to point to my public static IP (ADSL), which works great from the outside, but mixes things up while trying to access servers from the home network. I have figured out I'll have to setup a DNS server and overwrite the domains I serve and forward up to the ISPs everything else, but I wish there was an easier way of doing this. Yes, I could hack /etc/hosts, but I won't. The other downside of running at home is lack of reverse DNS lookups, but I think I can live with it.</p>
<p>In conclusion, I am overall extremely pleased with Debian, like I was with Ubuntu. I hope a few months of service, and I'll still be happy with it.</p>
