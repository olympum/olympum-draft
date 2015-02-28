---
layout: post
published: true
category : util
author: Bruno Fernandez-Ruiz
title: Nifty Minidrive Storage Hack
---

Adding storage to a Macbook Pro can be an expensive proposition given
the compact hardware architecture the new MBPs have. For my MBP
15-inch retina laptop, which comes with a 512 GB SSD, I wanted to add
a bit extra where to put all our Dropbox, GDrive, Box, etc. network
share replica. Nifty Minidrive is one of the most attractive options.

[Nifty](http://minidrive.bynifty.com/) is a young UK startup based out
of Manchester. Coming out of kickstarter fund raising, with the usual
manufacture out of China (possibly Shenzhen if I had to guess), they
have managed to create a very elegant, practical and beautiful way to
expand the storage for your laptop using the SD card slot.

Their Minidrive is a miniSD card reader with an SD form factor, so
that you can insert it into your SD card slot. I liked two things
about it: first, I can bring my own miniSD card which allows either
to get SDHC (a lot of storage) or SDXC (fast storage); second, once
inserted it does not stick out al all in the card slot.

I ordered the Nifty Minidrive from Amazon alongside a Samsung Pro
64 GB miniSD card (my researched showed this was the fastest and most
reliable one at least for my needs). The package arrived next day with
Prime:

![Amazon]({{ site.base_url }}/assets/nifty/amazon.jpg)

The Nifty guys have learnt a couple of lessons from Apple's beautiful
package, to make it a truly pleasant experience to open it and look
at the electronics:

![package]({{ site.base_url }}/assets/nifty/package.jpg)

I ordered the Minidrive for the MBP 15 Retina (each Macbook needs a
different Minidrive). The package included a Kingston 4GB miniSDHC
card, the Minidrive itself and a tool to help extracting the Minidrive
from the SD card slot (which conveniently also serves the purpose of
popping out the SIM card slot for the iPhone):

![contents]({{ site.base_url }}/assets/nifty/contents.jpg)

Pushing in the Samsung Pro card was straight forward, then insert it
into the SD card slot, and we are done with the Minidrive being
completely flush and not protruding at all:

![flush]({{ site.base_url }}/assets/nifty/flush.jpg)

The SD card slot is mounted as a USB storage drive. The Samsung card
came formatted as extended FAT but using DiskUtility I reformatted it
as MacOS Extended (Journaled, Not-Case Sensitive). It now shows up
permanently on my desktop.

A speed test of the Minidrive using the Blackmagic Disk Speed Test app
shows the promised sequential read and write speeds for the Samsung
miniSDXC UHS-I card, rated at 80 MB/s for writes, and 90 MB/s for
reads:

![speed]({{ site.base_url }}/assets/nifty/speed.png)

Overall I am very impressed with the little Nifty Minidrive. Although
there are other storage expansion options out there, I did not find
any other that was as easy and as elegant to use as the Minidrive. If
you need a bit more storage on your laptop, or perhaps a separate
drive for whatever purposes, I highly recommend the Nifty Minidrive.

