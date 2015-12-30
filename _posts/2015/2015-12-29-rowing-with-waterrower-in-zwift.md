---
layout: post
published: true
category : sports
author: Bruno Fernandez-Ruiz
title: Rowing with the WaterRower in Zwift
---
I have been rowing with the WaterRower indoor erg for a while, a good quality
home rower overall, but notoriously known for its complete lack of software
support. It is hard to get data out of it, it's hard to make it interface with ...
anything, and it is mentally exhausting. A bit like indoor cycling with a
turbo trainer was before Zwift. On the other hand, I have really enjoyed
riding indoors on Zwift almost daily for the past year. As I took back rowing
to work on my core, the itch became how to interface the WaterRower so that I
could row on Zwift using the power readings from the WaterRower S4 computer.

**tl;dr** a program to get [the WaterRower as a bluetooth power
meter](https://github.com/olympum/waterrower-ble) (on github).

## Let's Talk Power: Zwift, WaterRower, and Concept2

As background, Zwift works with power. No power, no movement. Power in Zwift
may be "true", measured directly from a power meter fitted to the bike, e.g.
from a torque reading, or from a smart trainer's active resistance. Power can
also be virtual and inferred from the trainer's resistance curve using the
wheel's revolutions and circumference (and possibly a number of other factors
such as temperature). This virtual power is what Zwift calls "zPower".

The WaterRower outputs power (watts) through a pretty accurate calculation
done on the S4 computer using the paddle speed. Next to the clutch, on top of
the water tank, there is a toothed wheel and an optical detector counting
pulses per revolution for the purposes of paddle speed measurement. With the
paddle speed and the water mass, the erg estimates angular velocity, total
work input (kJ) and power (watts). Since power is estimated from angular
velocity via an optical sensor, what the WaterRower S4 produces is somewhat
equivalent to the power readings the Elite Misuro B+ calculates for most of
Elite's "dumb" trainers. In a way, it's like zPower, but calibrated for a
fixed piece of hardware.

From my experience using both Concept2 and WaterRower ergs, the accuracy and
precision of the WaterRower is non-existent for pace, but it's quite accurate
when it comes to power. Non-scientifically, just from my personal experience,
the power readings from the WaterRower are very close to the Concept2 when
looking at average power for all-out efforts in 500m, 2000m, 5000m and 10000m.
Pace, on the other hand, is simply whacky. The one realy key technical benefit
the Concept2 direct force measurement has over the WaterRower optical sensor
is the ability to measure power throughout whole catch, drive and recovery
phases, and not just at the beginning of the catch. The other differences
between Concept2 and WaterRower are the drive technique, pressure on the knees
(C2) vs the lower back (WR), air (C2) vs water (WR), aesthetics, noise, etc.
but those are all factors not affecting power readings (although they may
affect the rower's efficiency).

_Ok, but I really want to see my 500m split pace!_ Well, if you really,
really, are interested in pace: it's possible to go from watts, as read by the
WR, to pace, using a simple formula (pace = (2.8/power)^(1/3) or [Concept2's
online watts
calculator](http://www.concept2.com/indoor-rowers/training/calculators/watts-calculator).

## The Path to a WaterRower Power Meter

My initial plan was to connect the WaterRower to the same machine I use for
Zwift. Unfortunately that did not work. The communication with the WaterRower
over USB (serial port emulation) seems to conflict with the communication
messages Zwift does over USB to ANT+, CompuTrainer ... Anyway, this seemed
complicated, so I decided to abandon this route and instead setup a dedicated
embedded device, e.g. an Arduino or a Raspberry Pi.

I opted for a dedicated Raspberry Pi since I had one around. With an RPi I
could just leave it running,  and automatically get the BLE sensor to start
advertising whenever I connect the USB cable to the WR.

Starting with the WaterRower side of things, using the serial port via USB,
things were easy since I had already written [a program to control the
WaterRower](https://github.com/olympum/oarsman). Unfortunately the go BLE
support was behind nodejs' `bleno` library. So I ported my old code to
Javascript, and the USB side of things was working pretty much immediately.

Next I had to figure out how to broadcast this data via radio. Initially, I
explored ANT+, but quickly gave up. Besides being a closed consortium
requiring certification, it just made no economical sense to me. A bluetooth
USB dongle costs less than $5 bucks. An ANT+ USB dongle is at least $10+. So I
picked Bluetooth 4.0 (LE/Smart) especially since Zwift was finally also
supporting BLE.

Little I knew all the issues that would come with BLE. Maybe ANT+ was not have
been such a bad idea. First, I found problems with Bluetooth LE in Linux. The
standard stack, `bluez`, did not support BLE well for a long-time during its
4.x series, and BLE only started being fully supported from version 4.99.
Right now, `bluez` is at 5.x and this is the version packaged in the latest
distros for Debian and Ubuntu. Unfortunately, the API between 4.x and 5.x have
changed quite a bit, as well as the kernel support. The library I am using for
BLE, `node-bleno`, is supporting `bluez` up to version 4.99, and it is not
fully working with the bluez 5.x series. To bypass this I figured we need to
shut down the bluetooth daemon and start the device manually, via `hciconfig`.

I could get BLE running and see the power, but only for a few seconds. BLE
would not work reliably: at some random point in time, the kernel would think
the USB bluetooth device was inactive, disconnect it and just immediately
after re-detect it and reconnect it. This recycling would happen randomly
whilst using the BLE. I found a bunch of problems with 4.x kernel
compatibility issues (the latest image for RPi), firmware issues for my
bluetooth dongle, ... deep sigh ...

Since this was a Friday night project, I just decided to bypass the problem
and break things into two programs: one doing the USB work, on the Raspberry
Pi, and one doing the BLE work, on a computer where BLE works reliably, e.g. a
Mac. I got them to communicate with each other over the network.

For the network side of things, I decided to use UDP multicast to send out the
WR data from the USB program to the BLE program. The datagrams are sent to
`224.0.0.1`, so a route must be setup in the Raspberry Pi and the Zwift
computer to accept multicast. The choice of address is done to leverage the
default route setup on Macs and Windows machines. UDP multicast makes
discovery easy, so that I don't need pass IP addresses around. UDP is also
lightweight and better suited for time-sensitive packets, like in games.
However, multicast is not a standard network setup, which might be a hurdle
for some people. Also, UDP is not reliable, so we may get dupes or missing
packets. We can deal easily with dupes using a sequence number. Missing
packets are a bigger problem though, since they show up as power drop on the
BLE sensor. I could add a re-transmission framework, and all the stuff, but
then what's TCP for? Or maybe we could do UDP only for discovery, and then TCP
for communication. In any case, packet loss in an internal LAN should not be a
problem for most people.

In summary, my setup so far was:

* The WaterRower S4.2 (S4.1 is the serial version, S4.2 is the serial over USB
  version) is connected via USB to the Raspberry Pi. There is also a new S4
  monitor, but I have no access to it. I don't think the protocol
  specification has changed though. The Pi is running Debian Jessie.
* Linux kernels 3.x and above support the serial over USB device. Instead of
  talking directly to the USB port, we use it's corresponding serial port,
  which offers a much simple ASCII-based interface. However, if you run this
  on Windows or Mac, you'll nee to install the Prolific PL2303 driver (Google
  it).
* The Zwift computer runs the other half of the program; it listens to the
  datagrams, and it forwards them on as a Bluetooth LE cycling power
  peripheral service. The computer obviously needs to have a Bluetooth 4.0
  USB adapter. All Macs since 2011 have this, and a dongle will cost you less
  than 5 bucks anyway.
* The Zwift companion app must be running on a phone with bluetooth, to pick
  the Bluetooth signal (that's a Zwift design constrain, they don't read BLE
  directly from the computer app, rather bridge through the BLE on the phone).
* The computer running the Zwift app must be on the same WIFI network
  as the phone (again, this is a Zwift constrain).

Success, it works! And it also works on other apps, not just Zwift, for
example on the Wahoo Fitness app for iOS, so that I can watch a movie on
Netflix whilst I row, and get the FIT file from the Wahoo app.

Yeay!

But the itch to run everything on the Raspberry Pi continued.

Investigating, I found that aside the bluez 4.x vs 5.x problems, the Raspberry
Pi is by design a very power constrained device, with imposes limits on the
power draw USB devices can do. The power draw of the bluetooth device and the
USB from the WaterRower is significantly more than your usual USB keyboard. To
solve this, I got myself a power supply providing a consistent 5V/2A, and I
configured the RPi to boot and allow drawing 1.2A from the USB, rather than
the default 0.6A.

And ... it works! I am now running without network mode, i.e the RPi is both
talking to the WaterRower via USB and exposing the readings as a Bluetooth LE
cycling peripheral. I have kept the network mode just in case others need it,
as unfortunately Bluetooth LE and Raspberry Pi don't go completely smooth just
yet.

Here's my son Hugo rowing on Zwift, including cat support:

![Hugo Rowing in Zwift]({{ site.base_url }}/assets/zwift/hugo-rowing.jpg)

And this is one of my longer rowing sessions on Strava:

<iframe height='405' width='590' frameborder='0' allowtransparency='true' scrolling='no' src='https://www.strava.com/activities/454828911/embed/dbcf39c7c9df98c26451297c105db839476f1c68'></iframe>

All I need now is rivers I can go on (maybe the "flying bug" that kicks once
in a while can be repurposed) and a single scull on Zwift :) For now whenever
I am on the erg, I use the Buffalo bike and the classic wheelset. Because they
are classy. Also, I can't use my hands to type whilst rowing, so no messaging
during my "rowing rides".

The code is in [github](https://github.com/olympum/waterrower-ble) and hope
others with a WaterRower may find it useful.

So, from now on, if you see me on a Buffalo bike at a silly cadence of 17-28
rpm ... please give me a Ride On!
