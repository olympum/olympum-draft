---
layout: post
published: true
category : sports
author: Bruno Fernandez-Ruiz
title: WaterRower vs Concept2 - A Power Study
---
There are many comparisons online between the two leading erg rowing machines, the Concept 2 and the WaterRower. There are many "soft" reasons discussed, but how do the two erg compare when it comes to pushing top watts? As a data-oriented athlete, I set myself to figure this out.
<img src="{{ site.base_url }}/assets/2017/04/rowers.png"/>

When I bought my WaterRower back in 2013, I spent time researching which erg rower to get for my home use. After narrowing it down to the WaterRower and the Concept2, I ended up choosing the WaterRower. Let me save you a few hours of researching forums, articles and blogs. These are the key "soft" differences between the ergs:

* The C2 resistance comes from a fan moving air; the WR resistance comes from a paddle moving water.
* The C2 resistance is linear and allows pushing as many watts as your muscles and heart will let you; the WR resistance is non-linear, and as you row harder you generate less incremental watts to the point of being impossible to generate more power. This is a big deal for athletes, but less of a concern for general fitness folks.
* The C2 is mechanic and noisy; the WR is fluid and silent (even a bit relaxing because of the sound of the water).
* The C2 rowers position is more natural, and puts more pressure on the knees; the WR position is less natural, but it is kinder on the knees, and harder on the lower back. Again, this is a big deal for athletes, less so for general fitness folks.
* The C2 has a superb ecosystem, software support, online community, training resources, rowing clubs use it, and it's usually available in gyms; the WR is very limited and almost no community (perhaps except for the spin-off Indo-Row).
* Adjusting the dampening (volume of air or water moved per stroke) in the C2 takes 2 seconds; in the WR you need to add and remove water and takes minutes.
* The C2 looks like a gym machine; the WR looks like a beautiful piece of home furniture.

Despite being interested in a rower for proper training, and not just basic fitness, we still decided to buy a WaterRower for our home use. This made sense, at least at the time, since I had plenty of opportunities of using C2s at the gym at work and in hotels whilst traveling.

When it comes to data, the data readings from any C2 machine are trusted across the community. In fact, using the Concept2 Utility application it is possible to automatically upload any session from a C2 rower equipped with a PM3, PM4 or PM5 monitor to the Concept2 Online Logbook, a community and global ranking of rowers. In contrast, the WR readings are considered bogus, and there is no software support, no community and no ranking for times on WR.

Since I row on the WR at home, and on C2s whilst I travel, my training log is full of power readings from both rowers. I really want to be able to compare apples to apples, and knowing how your power meters stack against each other is critically important.

Comparing power curves across this two rowers is a tricky business. Ideally, I should have a reference curve from a trusted power meter. Unfortunately, fitting an external power meter to either a WR or a C2 is not possible. I could also compare all-out 2k efforts from a group of athletes both on the WR and the C2. But I do not have such a group, nor I have enough 2k samples from myself to run a proper comparison.

The second possibility to compare power is to chart the critical power curves for both rowers. Unfortunately, I only have stream data (FIT/TCX) from the WaterRower (via my hacked RaspberryPi to read from the USB connection), as the C2 PM3/PM4/PM5 only records interval by interval summaries, rather than as a data stream (reminder to self, I must also hack the C2 ...).

Although not ideal, a good approximation of the power curves is to use heart rate to look at longer efforts, over 20 minutes long, rowing across UT2, UT1 and AT zones. I looked for rowing sessions from the past 6 months and plotted the average power and average heart rates. I then looked for the curve inflection point (using the same rationale as a Conconi test in cycling to estimate the anaerobic threshold).

The result is plotted below and unsurprisingly it confirms the mechanical resistance limitation that the WaterRower has.

<img src="{{ site.base_url }}/assets/2017/04/C2vsWR-deflect.png"/>

There are a few learnings we can derive from this chart:

* Between 180-210w both rowers perform approximately the same: same effort, same power output.
* As the drive and effort increases, the WR very quickly generates more power. There is in fact very little difference required in the WR to generate 200w or 230w.
* After 240w, it becomes much, much, much, harder to generate power in the WaterRower. Regardless of putting much more effort in, there is almost no increase in power output. This is likely due to the mechanical properties of the WaterRower.
* In the WR, I saw the curve inflection to happen at a LTHR of 151 bpm, which is much lower than what I know should be the case. This is because of the impossibility of driving more power on the WR.
* The C2 shows a much more linear response, and in fact, I did not reach my LTHR (as expected), and there is no inflection point in the curve.

In both the C2 and the WR, the power output generated is the product of multiplying the moment of inertia (which is a function of the water mass or the air mass) times the angular acceleration times the angular velocity. In the WR, the moment of inertia is constant since the volume of water in the tank does not change, whereas in the C2, the volume of air is unlimited. As the angular velocity increases, the torque required to generate more power becomes much harder in the WR than in the C2.

As summary, I believe the power output of the WR is overall not matching the output of a C2, whether that's for consistency or for accuracy.

1. For recreational rowing below 190w, the WaterRower provides a very good response and can be compared to a Concept2 rower. It is most likely though that this population is not bothered about the accuracy of the power readings from the WaterRower, for which the design criteria of the WR for comfort, noise, aesthetics, etc. are more important.
1. For steady efforts below 230w, the WaterRower provides a consistent, yet not comparable (accurate?) response to a Concept2 rower. The WR generates too much power, way too quickly.
1. For serious rowers able to pull 500m splits below 1:50, it is impossible to do VO2Max workouts on the WaterRower -not without increasing the stroke rate beyond what is reasonable and expected in the water, effectively destroying the rowing technique-, and the Concept2 is the only viable ERG.
