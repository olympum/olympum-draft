---
layout: post
published: true
category : sports
author: Bruno Fernandez-Ruiz
title: The Curious Case of the Elite Turbo Muin and Misuro B+
---
Elite's Turbo Muin is a super quiet direct-drive "classic" fluid trainer with a very smooth and progressive response. By classic Elite means it's not a "real" or a "smart" trainer, but rather that it has no resistance control and no power readings. To change resistance you gear up and down, and to get power readings we need to add a power meter. Elite however offers an optional Misuro B+ sensor for about $50 for its line of "classic" trainers which can output speed, cadence and power --the Elite Turbo Muin Smart B+ is nothing but a "classic" Turbo Muin with a built-in Misuro B+--. The question then is how good are the power numbers from a Turbo Muin with the Misuro B+?
<img src="{{ site.base_url }}/assets/2017/04/turbo-muin.jpg"/>

The Misuro B+ is a dual ANT+ and Bluetooth Low-Energy (BLE) sensor that can transmit speed, cadence and power depending on the trainer that it's connected to. For the first generation Turbo Muin, the Misuro B+ only transmits power, and for later post-2015 models it also broadcasts cadence, in addition to power.

<img src="{{ site.base_url }}/assets/2017/04/misuro_b_plus.jpg"/>

The Misuro B+ is not a "real" power meter, one that uses a strain gauge or similar mechanical device to measure torque directly. Rather, the Misuro B+ is a model-based power meter. The theory behind a model-based "power meter" is relatively simple, at least in principle. The trainer has a known resistance curve which is a function of the angular velocity, angular acceleration and moment of inertia of the rotating unit. Depend on the source of the resistance, the moment of inertia can be calculated as a function of the mass of oil moving inside the trainer (for fluid trainers), the mass of air flowing through the fan (as found in the LeMond's trainer), or from the brake's magnetic field force (as seen for example in the new KICKR). For a fluid trainer, the mass of oil is known in advance, hence if we can measure the angular velocity and acceleration for each rotation, we can then calculate the work and the power begin generated. There is a small metallic plate attached to a cog inside the TM that rotates as the belt turns, so that the Misuro B+ can detect every rotation using a magnet inside its casing. The Misuro B+ uses this rotation count to compute angular velocity and angular acceleration, and from that it derives torque, power, and finally broadcasts the computed readings via ANT+ and BLE.

I bought an Elite Turbo Muin in early 2015, right after starting [Nexar](https://getnexar.com) to have a trainer that I could use whilst working from our Tel Aviv office (at home I use a Wahoo KICKR). I had been using the TM for a year with my Garmin Vector pedals power meter as source of power readings, when Elite came out with the Misuro B+. I usually travel with my Vectors back and forth between home (UK) and work (Israel), which is a bit of a pain as the Vectors installation is quite finicky. I have had good experiences with model-based power readings, as found in the WaterRower and the KICKR, and the Misuro B+ looked like a promising option that could avoid me from having to uninstall, carry and reinstall my Vector pedals along every trip to Israel.

At least, that was the theory.

I set myself to test the consistency and accuracy of the Misuro B+ readings for the Turbo Muin. On one of my Zwift rides, I collected both the data from the Garmin Vector pedals (on Zwift) and the Misuro B+ (on my Suunto Ambit2).

<img src="{{ site.base_url }}/assets/2017/04/power.png"/>

There are quite a few interesting findings from plotting the two power curves alongside. As an average for the whole ride, the Misuro B+ reads 245 w compared to 231 w on the Vector pedals. This difference is within the accuracy advertised by Elite.

One interesting additional finding is that the power readings from the Misuro B+  slowly drift higher over time as the oil temperature increases and the sensor does not compensate for it.

<img src="{{ site.base_url }}/assets/2017/04/temp-drift.png"/>

If we zoom into the flat section at the beginning of the ride, we see that the Misuro B+ does in fact a remarkable job, at lower power numbers, and when cold.

<img src="{{ site.base_url }}/assets/2017/04/power-zoom-flat.png"/>

Because of the way power is measured, the Vectors readings fluctuate very fast, whereas the Misuro B+ provides a very smooth power curve. Both curves however track each other extremely well, with an accuracy error below 1%.

As we get to the hills and put down some serious power, the Misuro B+ starts over reading, by a lot. On the peak, the Misuro B+ reads 400w whilst the Vector pedals read 360w (10% off).

<img src="{{ site.base_url }}/assets/2017/04/power-zoom-hills.png"/>

In terms of rate of response, the Misuro B+ responds as fast as the Vectors. This is likely the case because the TM is a fluid trainer, and it needs more time to accelerate --this is why sprinting on the Turbo Muin is a no-go--. I would expect the Vector pedals to be more sensitive to power fluctuations and accelerations, but we can't observe that, at least not when connected to a Turbo Muin.

The difference in readings is more visible if we chart the distribution of power in a histogram.

* Both power meters agree most of the time in anything below 190w.
* Between 200w and 230w the Misuro B+ reads under the Vectors
* Between 230w and 260w, the Misuro B+ reads higher than the Vectors.
* Between 260w and 340w, the Misuro B+ reads under the Vectors.
* Beyond 340w, the Misuro B+ consistently reads over the Vectors.

<img src="{{ site.base_url }}/assets/2017/04/distribution.png"/>

When looking at these differences through a curve plotting critical power, we see that the Misuro B+ always read higher than the Garmin Vectors, and the higher the power, the higher the relative error.

* 20 minutes: 263w vs 279w (6%)
* 5 minutes: 301w 334w (10%)
* 1 minute: 353w 404w (13%)
* 5 seconds: 447w 529w (16%)

<img src="{{ site.base_url }}/assets/2017/04/cp.png"/>

In summary, the Misuro B+ is a good and cheap alternative to a real power meter, yielding accurate results within 5% error for steady endurance rides below 250w, which is the sweet spot for this fluid trainer. However, for riders who want to use this trainer and sensor combination to race on Zwift, or just for those looking for something accurate and consistent in harder interval workouts, the Misuro B+ is not the solution and should be looking into a real power meter instead.
