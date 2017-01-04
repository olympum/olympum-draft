---
layout: post
published: true
category : Sports
author: Bruno Fernandez-Ruiz
title: Are lighter riders faster on Zwift?
---
In Real Life (IRL) cycling, the laws of physics apply and determine
how fast we go. Do the same laws apply on Zwift, so that lighter
riders go faster on the climbs on Zwift?

We hear from heavier riders how lighter riders are at an advantage as
soon as the road goes up, and viceversa, lighter riders claim they
can't compete with heaver riders on the flats. That would be the case
IRL, is it so on Zwift?

A few weeks ago, I set myself to find out how weight and aero (using
height by proxy) impact times. This is becoming very important
recently as we manage many more group rides at Team WBR and need to
provide guidance to keep the group together. It is also good to know
for racing and for analyzing digital-doping on weight or height.

I ran the tests using my BLE power meter cycling simulator, which is
also what I use to connect the WaterRower S4 to Zwift. I tested on
Watopia Flat and Watopia Mountain routes using different weights and
heights, and always on a Zwift TT with Zipp 808/Disc wheels (I picked
the Zwift TT bike to avoid benefiting from draft during the tests).
The theory is that by fixing the bike and the wheels, the height
difference here is all that is affecting the aerodynamics.

## Absolute Power, Height and Aerodynamics

When we cycle in flat terrain in real life, the aerodynamic drag (air
resistance) is what determines how fast the bike travels. Drag is
impacted by the rider's size, position, bike's design, helmet, etc.
Weight however is not a factor impacting pace on the flats, at least
once the bike reaches cruising speed.

If IRL would apply to Zwift, we would expect to see:

* Given the same aero configuration, absolute power is the only factor
  that determines pace, which is independent of the rider's weight.
* Given the same absolute power and weight, given a bike and wheels
  kit, pace is only impacted by height.

To figure this out, I setup a virtual rider using the following
parameters:

* Height: 170cm, 180cm, 190cm
* Power: 200w, 300w
* Weight: 70kg, 80kg, 90kg
* Bike/Kit: Zwift TT, Zipp 808/Disc
* Route: Watopia Flat
* Strava segment: [TT Watopia](https://www.strava.com/segments/11193271)

The findings, which are shown on the table below, are not quite what I
expected:

1. <u>There is a 3.5% time penalty per 10kg of weight</u>. At
   200w, the heavier 90kg rider (170cm) is 39 sec slower, (7.66%). At
   300w, this difference is 6.8%. I expected the rider's weight not to
   impact segment times, since this is a flat segment where only aero
   and absolute power should matter.
1. Across the board, <u>there is approximately 5 secs penalty per 10cm
   of additional height</u>. I expected some impact of height, as the
   rider will have a harder time getting tucked into a good aero
   position, but the penalty is more than I thought.
1. There is a very strange anomaly here for 300w and 80kg. The 180cm
   rider is actually faster than the 170cm one, and the 190cm is
   approximately the same as the 170cm. I ran the tests twice, and the
   results seem consistent so I am not sure why this is happening.

<img src="{{ site.base_url }}/assets/2017/01/aero.png" style="width:700px"/>

## Dragging Your Weight

And this brings us to the mountain.  What happens when we go up? In
theory, here weight should be a significant factor. For the same
absolute power, the lighter rider should go up faster, since it
generates more watts per kilogram. That is the case in Zwift, but by
how much?

I wanted to find out the impact of weight:

* Given the same absolute power and aero configuration, the lighter
  rider generates more watts per kg and is therefore faster. By how
  much?
* Given the same weight and aero configuration, the rider with more
  power is faster. By how much?

I used the same settings as in the aero test to do a few laps of
Watopia Flat. The results for
the
[Watopia Ocean Road Lap Strava segment](https://www.strava.com/segments/11112480),
which are also available on the table below, are very interesting to
understand how Zwift's algorithms work:

1. <u>There is a 3% time penalty per 10kg of weight</u>, given the
   same aero (height) and power. For 200w, this is about 3.3% and for
   300w it goes down to 2.9%.
1. <u>There is a 15% time improvement per additional 100w of
   power</u>, given the same aero (height) and weight. This is
   consistent for all height and weight levels.

<img src="{{ site.base_url }}/assets/2017/01/weight-1.png" style="width:700px"/>

During these tests I came across something very intriguing that would
make me do further tests: at the same watts/kg (3.33 w/kg) and height
(170cm), the heavier rider was 30 seconds faster per Watopia Ocean
Road lap! Really? Why?

## Going Up, Up, Up

As this was very puzzling to me, I wanted to see what would happen on
a longer climb given the same relative watts per kg, but for heavier
and lighter riders. This time I setup the virtual rider to go around
the Watopia Mountain route, to look at the climb on the long EPIC KOM.
This time I used the following parameters for the tests:

* Height: 180cm
* Power (relative): 3.33 w/kg
* Power (absolute): 233w (70kg), 266w (80kg), 300w (90kg)
* Weight: 70kg, 80kg, 90kg
* Bike/Kit: Zwift TT, Zipp 808/Disc
* Route: Watopia Mountain
* Strava segment: [EPIC KOM](https://www.strava.com/segments/11596184)

The results are non-obvious to me:

1. The 80kg rider is 1.1% faster than the 70kg rider.
1. The 90kg rider is 1.8% faster than the 80kg rider (2.9% faster than
   the 70kg rider). Remember that the 90kg rider is putting 300w to go
   up, whereas the 70kg rider only needs 233w.  So, the finding here
   is that if you can support it with absolute power numbers, it's
   better to be big, rather than small, on the Zwift KOMs.

<img src="{{ site.base_url }}/assets/2017/01/ascent.png" style="width:700px"/>

## Going Fast on the Descent

What goes up, must go down, right? Ok, so how fast do we go down?
Again, same test parameters as with the ascent test. The results are
even more intriguing (for
the
[Mountain Descent Strava segment](https://www.strava.com/segments/11594714)):

1. The 70kg and 80kg riders are equally fast. This is good, since in
   theory we set the same aero drag by fixing bike/kit and height.
1. The 90kg rider is 2.9% faster than the 80kg one. Why?

<img src="{{ site.base_url }}/assets/2017/01/descent.png" style="width:700px"/>

## Summary

This has been a long post, but there are some important points I think
here, at least for us at Team WBR leading group rides:

* Setting a relative watts / kg target is the most efficient and
  accurate way of managing the group in Zwift. Speed and
  absolute power don't correlate well as w/kg for all terrains.
* At the end of the day, w/kg rule, not your weight or absolute power,
  even on the flats. This hopefully removes the whole lighter vs
  heavier rider debate; if a ride is at 3 w/kg, it does not matter
  what you or the rider leader weight, as long as both rider at 3
  w/kg.
* Heavier riders that can generate big watts have a significant
  advantage on the climbs, compared to lighter riders doing less watts
  but the same w/kg.
