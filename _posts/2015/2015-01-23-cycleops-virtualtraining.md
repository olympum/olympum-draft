---
layout: post
published: true
category : sports
author: Bruno Fernandez-Ruiz
title: Wahoo KICKR and CycleOps VirtualTraining
---

Since I bought the
[Wahoo KICKR](http://www.wahoofitness.com/devices/kickr.html), I have
been exploring the available software for it. Although I appreciate
the simplicity of the
[Wahoo Fitness app](https://itunes.apple.com/us/app/wahoo-fitness-bluetooth-powered/id391599899?mt=8&uo=4),
I miss having structured workouts. Ouf of the software programs I have
tried,
[CycleOps VirtualTraining](http://www.cycleops.com/virtualtraining/overview)
has become my tool of choice for training with the Wahoo KICKR.

![CycleOps VirtualTraining]({{ site.base_url }}/assets/vt/cycleops.PNG)

With my first trainer, the
[Elite Qubo Power Fluid](http://www.elite-it.com/en/products/trainers/indoor-trainers/qubo-power-fluid-0),
I was happily using [Golden Cheetah](http://www.goldencheetah.org) for
real-time indoor riding, as well as post-ride analytics. GC is a
fantastic program, and I still use it post-ride to do all the training
analytics, but the current lack of support for the KICKR meant I had
to look for an alternative for controlling the trainer during the
workouts.

The natural route should have probably been to switch
[TrainerRoad](http://www.trainerroad.com) for riding. Like GC, TR
provides structured training, through an extensive library of
thousands of workouts, with and without video -- just like GC does,
with [ErgDB](http://www.73summits.com/ergdb)--. The TR user interface
is really well done, very slick and well thought out in terms of the
cadence/power information being shown. You can just drag and drop a
Sufferfest video into the workout file and start riding.

While evaluating TR, I came across Cycleops VirtualTraining by
accident. I thought initially it would only support Cycleops trainers,
but they also support the KICKR and like TR or GC, they have a
"virtual powermeter" concept that maps wheel speed onto watts, based
on each trainer's powercurve. The second thing I had read is that it
was a Windows-only program, which would not work either. But in fact
have an iPad version.

Digging into VT, the software seemed to provide everything I wanted
and more, at similar subscription price as TR:

* support for structured workouts, including [the Sufferfest videos](http://www.thesufferfest.com),
* virtual video routes,
* freeride mode,
* online competitions, and,
* support for the iPad.

![Dashboard]({{ site.base_url }}/assets/vt/dashboard.PNG)

The only thing missing in VT against the competitors's products, like
[Tacx Cycling App](http://www.tacx.com/en/products/software/tablet-ios-android)
or [BKOOL Simulator](http://www.bkool.com/apps-bike/simulator), is 3D
rides. However, I think 3D rides are still a bit of a gimmick
(although I look forward to testing [Zwift](http://zwift.com), based
on my previous trials with BKOOL I remain skeptical of 3D training
software). Only time will tell ...

## Virtual Routes ##

Routes are the core of the program, and I guess where the name of the
software "virtual" comes from. Essentially, routes re-create an
outdoor ride indoors. The routes are loaded from recorded GPS data and
an optional video file which is somewhat kept in-sync with your ride
pace. VT adjusts electronically the resistance on the trainer based on
the virtual slope (grade) that comes out of the GPS track. VT then
uses the power measurement from the KICKR to infer the (virtual) speed
and movement on the course. Like its competitor software programs, VT
also works without a power meter and for non-electronically controlled
trainers. There it uses the speed curve to infer power. As a side
note, my limited experimentation with VT and my Elite Qubo fluid
trainer gave me very, very, strange virtual speed values, but for
whatever is worth, so did Elite's own application.

To train using "profile training", one starts by searching for a
route. Here you can filter by distance, slope, whether it has video,
etc.

![Route search]({{ site.base_url }}/assets/vt/route_search.PNG)

Once you search, it's possible to filter the results:

![Route filter]({{ site.base_url }}/assets/vt/route_filter.PNG)

and look at your saved (favorite) routes:

![Route favorite]({{ site.base_url }}/assets/vt/route_fav.PNG)

With a route selected, we go on to select a bike and an optional
virtual partner. Virtual bikes are a way to save configurations for
speed ratio, weights, etc. (you can only configure the bike gear/ratio
on the web interface):

![Virtual bike]({{ site.base_url }}/assets/vt/virtual_bike_setup.PNG)

as well as the sensors connected to the iPad. In my case, I am using a
Wahoo ANT+ dongle for the iPad2, to which I connect the Garmin GSC10
(only the cadence data is used), the KICKR and the Mio Fuse.

![Bike config]({{ site.base_url }}/assets/vt/virtual_bike.PNG)

It's worth mentioning that the optional virtual partner is a really,
really, cool feature. Essentially, you can ride against another VT
user that has already ridden the route. I find this is a great feature
to motivate you while training, and I usually look for somebody that
has the target power I am looking for in the training session. This
allows me to train a route in Z2, Z3, etc. I just need to find the
right partner.

![Virtual partner search]({{ site.base_url }}/assets/vt/virtual_partner_search.PNG)

Once you have route, bike and partner, it's time to ride. VT offers
two modes: training and racing. The difference between them is that
with racing your ride becomes public and you compete in the
leaderboard for the route, whereas in routes your ride does not come
up in the public leaderboards (although your ride is still public).

As once gets riding, VT shows a terrain map alongside a summary of the
key metrics, with instant values and averages for power, cadence, and
heart rate. I would love to see Intensity Factor (IF) and Training
Stress Score (TSS) like GC or Wahoo Fitness, but that's currently
missing. A nice tough is that we constantly see in the map the
position of our virtual competitor as well as their position ahead of
behind us.

![Route map view]({{ site.base_url }}/assets/vt/route_map.PNG)

We can switch to the video view, which remains synchronized with the
map:

![Route video]({{ site.base_url }}/assets/vt/route_video.PNG)

It's worth mentioning that VT supports AirPlay, so we can send the
video stream to an AppleTV and keep the metrics view in the iPad. I
prefer to mirror the display and see the cadence and power metrics all
the time.

![Route metrics]({{ site.base_url }}/assets/vt/route_metrics.PNG)

Once we complete the ride, VT uploads and shares automatically the
ride onto multiple sites, e.g. Strava, and you can also get it to send
a .FIT file with the ride data, which will include the GPS track. VT
posts activities to Strava as private, so if you want to show them you
have to make them public and decide whether to keep or remote the GPS
track, i.e. appear on the segment leaderboards.

![Route summary]({{ site.base_url }}/assets/vt/route_summary.PNG)

VT does some basic analytics and charts/reports, which I don't quite
care for since I use GC, but they might be useful for some:

![Route graph]({{ site.base_url }}/assets/vt/route_graph.PNG)

Overall the virtual route functionality is well finished. There are a
few rough points though:

* Some of the routes have not been smoothed out, and there are too
  many frequent changes of slope / resistance that make riding on the
  KICKR quite a pain.
* Another issue that I have found is that not all videos are equally
  "smooth". Essentially, it depends at which speed the video was
  taken, whether it was closer to car speed or cycle speed.
* A couple of times, the downloaded video has gotten "stuck", and I am
  not sure why that is, nor whether this is also a problem with the
  stream.

![Video stuck]({{ site.base_url }}/assets/vt/video_stuck.PNG)

* I've also seen sometimes significant mismatch and gaps between the
  map and the video, sometimes even upto 30 seconds (it's easy to see
  this in changes of slope or when taking turns).
* Once every couple of rides, VT stops collecting data and disconnects
  from the KICKR for a few seconds, when no cadence, power or heart
  rate is collected. I have not been able to diagnose whether it's the
  KICKR, the iPad, the Wahoo ANT+ dongle or VT having the problem.

But in all, the features in the virtual ride make my current
subscription worth it, especially since the program also allows me to
follow structured workouts (like I would do in GC).

## Workouts ##

The structured workout functionality in VT is quite standard. Pick the
workout, pick the media / video file, and get going. For some of the
workouts, the video is automatically selected based on the "original"
file name, e.g. if the you have Sufferfest video on the iPad, VT will
find it and use it.

With workouts with video, all you really get is the video and power
(target % of FTP and actual % of FTP). I would hope to see cadence,
TSS, IF, like we do in the routes, but I guess it may come in a future
release:

![Workout with video]({{ site.base_url }}/assets/vt/workout_sufferfest.PNG)

In workouts without videos we get more data and a nice chart:

![Workout without video]({{ site.base_url }}/assets/vt/workout_no_video.PNG)

Like in the routes, once we complete, we get a summary page:

![Workout complete]({{ site.base_url }}/assets/vt/workout_complete.PNG)

and a similar analytics chart to the one we had in the virtual routes:

![Workout graph]({{ site.base_url }}/assets/vt/workout_graph.PNG)

## Freeride ##

The last ride mode of VT is freeride. This is a basic mode where we
can set the target power and VT adjusts the resistance to our cadence,
so that the power generation is constant.

![Freeride]({{ site.base_url }}/assets/vt/freeride.PNG)

And like in workout, we can select some media and watch it while we
ride.

![Freeride with video]({{ site.base_url }}/assets/vt/freeride_video.PNG)

I prefer however to do the ride without video so that I can see the
heart rate, power and cadence metrics.

Freeride also allows us to set the grade (slope) and then it basically
behaves like a fluid trainer, where the power we generate depends on
our cadence.

![Freeride with grade]({{ site.base_url }}/assets/vt/freeride_grade.PNG)

## Summary ##

CycleOps VirtualTraining for iPad provides a good solution for riding
with the Wahoo KICKR. At $5.99/month subscription, it's a good deal,
very competitive with competing solutions. I would like to see some of
the issues I have experienced addressed, e.g. video-route syncing,
power drop-outs, etc. but overall, it's a good program and I am happy
to use it.

