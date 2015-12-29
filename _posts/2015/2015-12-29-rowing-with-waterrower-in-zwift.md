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
meter on github](https://github.com/olympum/waterrower-ble).

As background, the way Zwift works is by using power as the source of truth.
Power in Zwift may come from a power meter fitted to the bike, usually
measuring torque, from a smart trainer exercising a resistance against the
movement, or from a class speed (and cadence) sensor, e.g. Garmin SC10,
through something Zwift calls "zPower", or a virtual power reading inferred by
using the wheel's speed and the trainer's resistance curve -- remember that
power = force * speed -- .

The WaterRower can measure power (watts), so it could theoretically appear as
as a cycling power meter, if only I could get the data out of the WaterRower
computer. Now, mechanically speaking, the WaterRower has a toothed wheel and
an optical detector counting pulses per revolution for the purposes of paddle
speed measurement. The WaterRower computer, the S4 monitor, uses this to
calculate angular velocity, and from this and the water mass, it estimates
total work input (kJ) and power (watts). It is important to remember though
that because of the way power is measured via an optical detector, rather than
direct force, the power readings are really only available at the end of the
catch, i.e. once per stroke. In summary, what the WaterRower S4 produces is
equivalent to "zPower", but with the difference that it's highly calibrated
and accurate for the S4.

From my experience using both Concept2 and WaterRower ergs, the accuracy and
precision of the WaterRower is non-existent when it comes to pace, but it's
fairly good for power. Power readings is somewhat comparable to the Concept2,
whereas pace is simply whacky. In any case, I prefer to train indoor with
power, even for rowing, and not pace.

Because of the pace issues in the WR, I have focused on just solving the
problem of getting power and cadence out of the WR. Now, if you really,
really, are interest in pace: it's possible to go from watts, as read by the
WR, to pace as 500m time splits, using [Concept2's online watts
calculator](http://www.concept2.com/indoor-rowers/training/calculators/watts-calculator)
which is just a simple formula (pace = (2.8/power)^(1/3)).

My initial plan was to connect the WaterRower to the same machine I use for
Zwift. Unfortunately that did not work. The communication with the WaterRower
over USB (serial port emulation) seems to conflict with the communication
messages Zwift does over the USB to ANT+, CompuTrainer ... Anyway, this seemed
complicated, so I decided to abandon this route and instead setup a dedicated
embedded device, e.g. an Arduino or a Raspberry Pi.

I opted for a dedicated Raspberry Pi since I had one around. With an RPi I
could just live it running,  and automatically get the BLE sensor to start
advertising whenever I connect the USB cable to the WR.

Starting wit the WaterRower side of things, using the serialport via USB,
things were easy since I had already written [a program to control the
WaterRower](https://github.com/olympum/oarsman). Unfortunately the go BLE
support was behind nodejs' `bleno` library. So I ported the code to node and
the USB side of things was working pretty immediately.

Next was to figure out how to broadcast this data via radio. I explored ANT+
first, but quickly gave up. Besides being a closed consortium requiring
certification, it just made no economical sense to me. A bluetooth USB dongle
costs less than $5 bucks. An ANT+ USB dongle is at least $10+. So I picked
Bluetooth 4.0 (LE/Smart) especially since Zwift was finally also supporting
BLE.

Little I knew all the issues that would come with BLE. First, I found problems
with Bluetooth LE in Linux. The standard stack, `bluez` did not support BLE
well for a long-time in its 4.x series, and BLE only started being partially
supported form 4.99. Right now, `bluez` 5.x is finally supporting BLE and has
become the standard package version in Debian and Ubuntu. Unfortunately, the
API between 4.x and 5.x changed quite a bit, and so did the kernel support.
The library I am using for BLE, `node-bleno`, is supporting `bluez` up to
version 4.99, and it is not fully working with the bluez 5.x series. To bypass
this I figured we need to shut down the bluetooth daemon and start the device
manually, via `hciconfig`.

I could get BLE running and see the power, but only for a few seconds. BLE
would not work reliably: at some random point in time, the kernel would
disconnect the Bluetooth USB device and just immediately after redetect it and
reconnect it. Research showed 4.x kernel compatibility issues (the latest
image for RPi), firmware issues for my bluetooth dongle, ... deep sigh ...

I just decided to bypass the problem and break things into two programs: one
doing the USB work on the Raspberry Pi, and one doing the BLE work, on a
computer where BLE works reliably, e.g. a Mac. I get them to communicate
with each other over the network.

For the network side of things, I decided to use UDP multicast to send out the
WR data from the USB program to the BLE program. The datagrams are sent to
`224.0.0.1`, so a route must be setup in the Raspberry Pi and the Zwift
computer to accept multicast. The choice of address is done to leverage the
default route setup on Macs and Windows machines. UDP multicast makes
discovery easy, and is lightweight and better suited for time-sensitive
packets, like in games. However, multicast is not a standard network setup,
which is a hurdle for some people. Also, UDP is not reliable, so we may get
dupes or missing packets. Dupes we can deal with easily with a sequence
number. Missing packets are a problem, since they show up as power drop on the
BLE sensor. Maybe we can do UDP for discovery, and TCP for communication (as
our latency requirements are not the same as in a shooting game). In any case,
it's not a big problem.

In summary, my current setup so far was:

* The WaterRower S4.2 (4.1 is the serial version, 4.2 is the serial over USB
  version) is connected via USB to the Raspberry Pi. The Pi is running Debian
  Jessie.
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

Success, it worked! And it also worked on other apps, not just Zwift, for
example on the Wahoo Fitness app for iOS, so that I could watch a movie on
Netflix whilst I row, and get the FIT file from the Wahoo app.

Yeay!

But the itch to run everything on the Raspberry Pi continued.

Investigating, I found that aside the bluez 4.x vs 5.x problems, the Raspberry
Pi is a very power constraint device, with embedded limits on the power draw
USB devices can do. The power draw of the bluetooth device and the USB from
the WaterRower was significantly more than you usual USB keyboard. To solve
this, I got myself a power supply providing a consistent 5V/2A, and I
configured the RPi to boot and allow drawing 1.2A from the USB, rather than
the default 0.6A.

Well ... it worked! I am now running with no network mode. The RPi is both
talking to the WaterRower via USB and exposing the readings as a Bluetooth LE
cycling peripheral.

And to prove it, you can see my son Hugo rowing on Zwift (with cat support):

![Hugo Rowing in Zwift]({{ site.base_url }}/assets/zwift/hugo-rowing.jpg)

And one of my long rowing sessions on Strava:

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
