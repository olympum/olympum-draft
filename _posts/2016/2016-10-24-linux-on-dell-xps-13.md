---
layout: post
published: true
category : Linux
author: Bruno Fernandez-Ruiz
title: Linux Desktop on a Dell XPS 13
---

It has been over 22 years since I started using Linux as my main operating
system. Back in 1994, I started with Slackware 2.1, and kept using Linux as
my desktop at school, for research, and even at work on a dual boot environment.
I spent countless hours then configuring the kernel, X11 and what not to make
things work. I went through distribution after distribution, till 2005, when
our eldest daughter was born, that I got tired of compiling Gentoo packages
and dealing with all the Linux issues. I had no time for it any longer.

In 2005, I switched to Mac OS X, and I have been a user till today, at home and
at work. I just did not have the time to deal with Linux, nor the patience to
learn and keep maintaining Windows PCs at home. And now the whole family is on
Apple, OS X and iOS, on Macbook Airs, Minis, Pros and what-not.

And honestly, it just mostly works, it requires very little maintenance and,
well ... Bob's My Uncle.

Or not. I had several reasons to try moving back to Linux. First, all our
development and production servers run Linux. And as much as I could run virtual
machines, there is always an overhead, not so much nowadays on the resources,
but on the mental switching cost. Additionally, a lot of the work has to do with
GPUs, so the ability to have a native desktop environment with Linux to either
do local development or remote development over a good X11 session is important.
At the end of the day, my "core" machine is a server or a beefy workstation to
which I connect remotely. What I want is a local desktop development environment
which mimics as much as possible my Linux servers. I use remote X11 sessions,
VNC and ssh, which I know I can also use with Quartz on Mac. But honestly, it's
significantly sub-standard to a native experience. No matter how much you like
Macports or Homebrew, Mac is not Linux. And I like Debian's APT.

Second, I wanted "better" hardware than the Macbook Pro Retina 15 I am using.
Although it might seem strange, I am not that impressed with the MBPr15. Yes,
it's a fine design, and yes, it all works. Battery life is sub-standard and the
way the kernel drives the NVIDIA card is buggy. And as much as Apple's next MBP
might turn up to be amazing, one must remember that there is a huge price
premium you pay for it. For the price of a new MBPr15 I can buy two and half
Dell XPS 13.

Third, I wanted to see whether using Linux would be different, easier, this
time. Would it still be a pain and lot of work to run Linux on a laptop, like it
used to be? Would I have to deal with firmware, proprietary drivers, unsupported
hardware, etc. issues?

As it happens, I am writing this post on my Dell XPS 13 (Skylake), which I
totally love. I am running Ubuntu 16.10 on a 4.8 series kernel. Everything
works. I am using a native and fast UEFI boot, at full screen resolution, sleep
and hibernation working perfectly, touchpad with multi-finger gestures, audio
working great, and all hooked up to my Apple LED Cinema Display via a Dell DA200
docking station. It is a gorgeous experience and I am simply loving it.

I have managed to replace almost every single tool on OS X for a Linux
application. A large reason for this is that so much of what we do at Nexar runs
on the cloud, on Google's servers. There is very little reason to have a lot of
desktop applications installed. In fact, I considered the Google Pixel2, which
is a fine piece of hardware, but at the end decided to go for a Dell XPS 13
since hardware compatibility seemed guaranteed. Although I use mostly web apps,
I still have a few native apps on my GNOME desktop environment (I tried KDE
Plasma, but I guess KDE and I don't agree on the desktop paradigm philosophy,
which is fine). Even my Suunto Ambit2 GPS watch works with Linux.

When I first got the Dell XPS 13, I installed Mac OS X as a guest on VirtualBox,
since I was fearing I could not access our presentations, done with Apple
Keynote. However, since then we have moved them to Google Slides, so all good on
that front. Plus they are much easier to share, modify, edit, etc. and they use
way less storage. The second reason for the OS X guest was the Apple Keychain
Tool, where I stored all my passwords. I am slowly migrating to [SpiderOak
Encryptr](https://spideroak.com/solutions/encryptr) as a multi-platform password
management tool, but till then I need occasionally access to the keychain. I
have found that I can see my passwords on the iPhone's Safari settings, so I
have not had a need to run the OS X VM for a month, and I just actually deleted
it.

There are however a couple of apps that do not work on Linux via a VM. I have
kept using the MBPr15 for Xcode, which also helps on those occasions when I need
access to an older Keynote deck. The other app I need is Zwift, which I am now
running either on the MBPr15 or on Windows, running on a small partition on the
Dell.

Altogether, I am excited and happy. I think as a portable desktop experience
the Dell XPS 13 running linux is probably one of the best available
environments, especially if you are a developer like me who needs to be on the
road quite frequently, but still check out and compile code here and there.
