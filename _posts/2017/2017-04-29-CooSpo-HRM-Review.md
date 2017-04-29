---
layout: post
published: true
category : sports
author: Bruno Fernandez-Ruiz
title: CooSpo H6 ANT+ and Bluetooh Heart Rate Monitor
---
Tired of my Wahoo TICKR Run failing to capture correct HR data in now almost every outdoor run, I decide to try something else. But given my positive experience with the Milestone Pod, instead of going for the usual suspects from POLAR, Suunto or Garmin, this time around I decided for a sub $30 Heart Rate Monitor and got a CooSpo. How did it fair?
<img src="{{ site.base_url }}/assets/2017/04/coospo_h6.jpg"/>

My experience with the Wahoo TICKR Run has been mixed. As a heart rate monitor, it served its purpose extremely well for 2 years of daily use. Battery, consistency and quality are really excellent when it comes to reading heart rate data, including R-R for HRV estimation. Recently I have experienced complete misreadings, either entering a classic plateau for a long period of time, or even worse, misreading by +/- 20 bpm randomly. As for its running dynamics features, I have never been able to use it properly. The running dynamics features only work if you use the Wahoo Fitness app. And even ignoring the running dynamics, the stride sensor is totally bogus and can read up to 5x higher or lower than correct, despite calibration. If you want a proper footpod, get the POLAR or the Milestone POD (highly recommended!).

In any case, I set to find a replacement and came across the CoosPo H6 HRM with dual ANT+ and BLE support on Amazon UK for £21.99 ($29.99 on Amazon.com).

The packaging is simple and straight forward.

<img src="{{ site.base_url }}/assets/2017/04/coospo.png"/>

Pairing the HRM either on Bluetooth or on ANT+ is straight forward. Here I have paired it with the Wahoo Fitness app over Bluetooth.

<img src="{{ site.base_url }}/assets/2017/04/coospo_ble_pairing.png"/>

In comparison with the Wahoo TICKR, the sensor is a bit "fatter":

<img src="{{ site.base_url }}/assets/2017/04/coospo_vs_tickr.png"/>

Anyway, time to compare the monitors. I paired the CooSpo with my Suunto Ambit2 over ANT+, the Wahoo TICKR with the Wahoo Fitness iOS app over BLE, and went out for a jog around the block. Upon download of the FIT file for the Ambit2, I found the summary rather "strange":

<img src="{{ site.base_url }}/assets/2017/04/coospo_fit_summary.png"/>

When looking at the data track, I saw the HR apparently dropping continuously:

<img src="{{ site.base_url }}/assets/2017/04/coospo_fit_hr.png"/>

As I looked deeper into the raw data editor in GoldenCheetah, I noticed this is an artifact of how Suunto captures the GPS data (I have not seen this elsewhere). Essentially, the GPS sampling is every 1 second, and when that happens the data point in the FIT file has latitude, longitude and altitude, but no dynamic data (no HR, no cadence, nothing). This seems to be corrected on the TCX export from Suunto's Movescount:

<img src="{{ site.base_url }}/assets/2017/04/coospo_tcx_summary.png"/>

Ah, better! Back to business, the same summary of the run from the Wahoo Fitness iOS app:

<img src="{{ site.base_url }}/assets/2017/04/tickr_summary.png"/>

As we can see the Wahoo TICKR records higher data: average 152 bpm (vs 151 bpm), and max 169 bpm (vs 165 bpm). But if we dive into the data comparing the CooSpo (magenta) with the TICKR (cyan), we see an odd behavior of the TICKR (at least my model, and this is with a fresh battery):

<img src="{{ site.base_url }}/assets/2017/04/tickr_vs_coospo_run.png"/>

There are two observations I would make. First, the TICKR has plateau sections, and even out of them it seems less responsive to changes than the CooSpo. Second, even when both HRM are tracking each other closely, the Wahoo read 2 to 3 beats below the CooSpo.

I also wanted to see the performance for indoor cycling on the trainer for Zwift (CooSpo on cyan, TICKR on magenta):

<img src="{{ site.base_url }}/assets/2017/04/tickr_vs_coospo_bike.png"/>

Unlike in outdoor running, things match quite well. If anything, there TICKR is slower to react and tends to read 2~3 beats below (similar behavior to running).

Looking at the R-R data, the CooSpo shows not recording gaps or jumps, which is critical for being able to use all the FirstBeat algorithms that POLAR, Suunto, Garmin and others use to calculate Training Effort, calories burnt, recovery times, etc.

<img src="{{ site.base_url }}/assets/2017/04/coospo_hrv.png"/>

I don't know why my TICKR exhibits this odd behavior. It might be that this is related to my singular unit, since as I mentioned the running dynamics and the stride sensor never worked properly, so perhaps the accelerometer inside is also affecting the heart rate readings. This would explain why I don't observe the odd behavior indoors, given the much larger body movement whilst outdoors.

Overall, regardless of the performance of the TICKR, and lacking EKG equipment to benchmark things, I can recommend the CooSpo. I have had it now for 2 weeks of daily use without any issues at all. Let's see how long it lasts.
