---
layout: post
published: true
category : sports
author: Bruno Fernandez-Ruiz
title: WaterRower vs Concept2 - A Power Study
---
When I bought my WaterRower back in 2013, I spent time researching which erg rower to get for my home use. After narrowing it down to the WaterRower and the Concept2, I ended up choosing the WaterRower. There are many comparisons online between the two so I will not go into details here. But to save you a few hours of reading:

* The C2 resistance comes from a fan moving air; the WR resistance comes from a paddle moving water.
* The C2 resistance is linear and allows pushing as many watts as your muscles and heart will let you; the WR resistance is non-linear, and as you row harder you generate less incremental watts to the point of being impossible to generate more power. This is a big deal for athletes, but less of a concern for general fitness folks.
* The C2 is mechanic and noisy; the WR is fluid and silent (even a bit relaxing because of the sound of the water).
* The C2 rowers position is more natural, and puts more pressure on the knees; the WR position is less natural, but it is kinder on the knees, and harder on the lower back. Again, this is a big deal for athletes, less so for general fitness folks.
* The C2 has a superb ecosystem, software support, online community, training resources, rowing clubs use it, and it's usually available in gyms; the WR is very limited and almost no community (perhaps except for the spin-off Indo-Row).
* Adjusting the dampening (volume of air or water moved per stroke) in the C2 takes 2 seconds; in the WR you need to add and remove water and takes minutes.
* The C2 looks like a gym machine; the WR looks like a beautiful piece of home furniture.

We went for the WaterRower for home, since I would have plenty of chances of using C2s at the gym and whilst traveling.

Because of the reasons above, the C2 data readings are trusted across the community, whereas the WR readings are considered bogus. Since I row on the WR at home, and on C2s whilst I travel, I really wanted to know how do these two rowers compare power wise.

Comparing power curves is a tricky business. Ideally, one should compare all-out 2k efforts from a group of athletes both on the WR and the C2. I did not have such a group, nor enough 2k samples from myself.

The second possibility to compare power is to chart the critical power curves for both rowers. Unfortunately, I only have stream data (FIT/TCX) from the WaterRower (via my hacked RaspberryPi to read from the USB connection), as the C2 PM3/PM4/PM5 only records interval by interval summaries, rather than as a data stream (reminder to self, hack the C2 ...).

Although not ideal, a good approximation of the power curves is to use heart rate to look at longer efforts, over 20 minutes long, rowing across UT2, UT1 and AT zones. I looked for rowing sessions from the past 6 months and plotted the average power and average heart rates. I then looked for the curve inflection point (using the same rationale as a Conconi test in cycling to estimate the anaerobic threshold).

The result is plotted below and unsurprisingly it confirms the mechanical resistance limitation that the WaterRower has. The plot infers

<img src="{{ site.base_url }}/assets/2017/04/C2vsWR-deflect.png"/>

There are a few learnings we can derive from this chart:

* Between 180-210w both rowers perform approximately the same: same effort, same power output.
* As the drive and effort increases, the WR very quickly generates more power. There is in fact very little difference required in the WR to generate 200w or 230w.
* After 240w, it becomes much, much, much, harder to generate power in the WaterRower. Regardless of putting much more effort in, there is almost no increase in power output. This is likely due to the mechanical properties of the WaterRower.
* In the WR, I saw the curve inflection to happen at a LTHR of 151 bpm, which is much lower than what I know should be the case. This is because of the impossibility of driving more power on the WR.
* The C2 shows a much more linear response, and in fact, I did not reach my LTHR (as expected), and there is no inflection point in the curve.

In both the C2 and the WR, the power output generated is the product of multiplying the moment of inertia (which is a function of the water mass or the air mass) times the angular acceleration times the angular velocity. In the WR, the moment of inertia is constant since the volume of water in the tank does not change, whereas in the C2, the volume of air is unlimited. As the angular velocity increases, the torque required to generate more power becomes much harder in the WR than in the C2.

As summary, what this comparison highlights is that the power output of the WR is indeed not matching a C2, except for recreational rowing around 190w. This is probably as expected given the other design criteria of the WR, for comfort, noise, aesthetics, etc.
