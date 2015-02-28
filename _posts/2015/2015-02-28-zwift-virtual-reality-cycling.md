---
layout: post
published: true
category : sports
author: Bruno Fernandez-Ruiz
title: Zwift - A Virtual Reality Cycling Game
---

This morning I received my invite into the Zwift Beta. Zwift is a new
3D cycling game which makes riding your bike indoors a lot of fun. 
Traditionally, I have been skeptic of 3D virtual riding, based on
my experience with BKOOL's and Tacx' products.  Zwift has managed
however to really add a true competitive gaming angle into
indoor riding.

![Zwift]({{ site.base_url }}/assets/zwift/zwift.png)

After downloading the DMG, installing the app for Mac OSX is straight
forward. Interestingly, as you fire the app, it behaves like a normal
Mac app, with an icon and a menu "Zwift". However, if we switch apps,
e.g. to a browser and come back, we see it's now called "ZwiftApp" and
the icon is now the default "exec" (the basic app in XCode). This
ZwiftApp has a Preferences menu option, but that brings the "GLUT"
preferences (an OpenGL utility toolkit?). It's probably just a small
cosmetic bug which you won't notice anyway unless you are like me
taking screenshots for blogging ...

![GLUT]({{ site.base_url }}/assets/zwift/glut.png)

Anyway, back to cycling and the game ... The first time we launch Zwift
we are asked to signup for the service. The screen is straight
forward, except for the "Promo Code" field in the form, which I assume
is for when the app goes out of Beta. I would hidden this field for the
time being, and only show it once the app goes out of beta and the
promo code actually means something. Or if it means something now,
hovering tips would be nice.

![signup]({{ site.base_url }}/assets/zwift/signup.png)

Right now you can only signup and create a username and password
combination on the app, not on the website. When you come back to the
app, you'll be faced with a login window, every single time you fire
up the app (which I found rather annoying):

![login]({{ site.base_url }}/assets/zwift/login.png)

Once we have signed up we can start to customize our player. As any
good game, there are items that we only unlock later in the game, as a
loyalty reward for playing and sticking around.

![customize]({{ site.base_url }}/assets/zwift/customize.png)

After customizing, we can pair our devices really easily:

![pairing]({{ site.base_url }}/assets/zwift/pairing.png)
![paired]({{ site.base_url }}/assets/zwift/paired.png)

Now, we are ready to start. We can either ride solo or join a friend.
I am unsure what friends are in this context, and I assume an
explanation will come soon, or an ability to connect to social
networks like Facebook or Strava.

![start]({{ site.base_url }}/assets/zwift/start.png)

Since I seem to have no friends, at least in Zwift, I started with the
"Just Ride" option. The experience is truly amazing, in the graphics
and the audio (which is nice and subtle). The details are very well
taken care of, and at least with a MBP 15-inch Retina late 2014, the
app runs very smoothly.

![riding]({{ site.base_url }}/assets/zwift/riding.png)
![riding2]({{ site.base_url }}/assets/zwift/riding2.png)
![riding3]({{ site.base_url }}/assets/zwift/riding3.png)

The experience is beautiful and the gaming aspects are very well taken
care of. On the right hand side, we see the players that are just
ahead and behind us. We also see their power to weight ratio, which is
useful to know for deciding if or who to draft. There are trophies
along the ride in the form of jerseys we get to wear immediately. I
could unlock climbing, sprint and lap, not sure if there are more.
This competitive side of the game really kept me going trying to beat
the other players!

I had a few issues with ANT+ though, which is not unusual nor specific
to the Zwift app anyway. I am using a Suunto ANT+ USB2 dongle, and I
was experiencing continuous dropouts and disconnects from the KICKR,
the GSC10 and even the Mio Fuse. Once the power reaches zero, the app
figures out in a few seconds that you have paused:

![dropout]({{ site.base_url }}/assets/zwift/dropout.png)
![pause]({{ site.base_url }}/assets/zwift/pause.png)

After some experimentation (the laptop and the dongle are only 1 ft
away from the KICKR), and some intutition from my previous experience
with USB to serial programming for the WaterRower S4, I figured out
that either the Garmin Connect or the Suunto Moveslink app were
getting on the way (the PL2303 driver for mac is very finicky). After
killing all apps that I knew were using the PL2303 driver, things
worked very smoothly from a power and cadence perspective, although
for some reason I lost the connectivity with the Mio Fuse.

Once we are done, the app saves the ride and exits. I figured at this
point I may want to visit the Zwift web app, called the "Dashboard". I
found there my rides saved:

![dashboard]({{ site.base_url }}/assets/zwift/dashboard.png)

We have an option to download the activity as a .FIT file, or to
connect with Strava. It would have been nice to see the connect with
Strava option earlier in the client, as I had to download the .FIT
file and upload it manually to Strava. In any case, my second ride
showed fine in Strava:

![strava]({{ site.base_url }}/assets/zwift/strava.png)

I am sure there is some excitement from the game's novelty. But
overall, this was one of the most enjoyable indoor rides I have ever
done and definitely worth the subscription whenever it comes out of
beta. I am not sure though I am ready to fully give up the video
virtual rides or the Sufferfest videos I get with
[CycleOps VirtualTraining](http://www.olympum.com/sports/cycleops-virtualtraining/).
I also want to see how the Zwift guys implement structured workouts,
which is definitely a must-have feature for me.

In summary, my kudos go to the Zwift team for figuring out how to
gamify indoor riding. The app nails the competition dynamics, all
within a world-class 3D experience. The Zwift product management team
has clearly been looking very closely (and copying, which is a good
thing) how Strava has built its community. I look forward to future
releases and wish success to this amazing sports gaming startup.
