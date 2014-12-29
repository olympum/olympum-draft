---
layout: essay
published: true
author: Bruno Fernandez-Ruiz
title: The User Data Marketplace
date: 2014-12-29
---

There is a nascent and potentially large opportunity to create a user
data marketplace, whereby users have full control of which and how
their personal data is collected and used.

## The Consumer View

Our activity on the Internet leaves behind a trail of behavioural
events from which information inference can occur: what we buy, what
we visit, what we read, etc. Hundreds of players on the Internet
collect these behavioural events in order to apply complex algorithms
and convert the raw behavioural events into valuable information. Ad
networks, ad exchanges, data management platforms, demand-side
platforms, personalization providers, app developers, cell networks,
data clearing houses, spy agencies, etc. The derived information is
used to optimize what each Internet player is trying to achieve:
publishers seek to improve engagement and yield; marketplace operators
seek better margins; advertisers look for optimizing the return on
investment for their marketing budgets driving awareness and/or
conversions; and finally, consumers are attracted by interesting
experiences that keep them engaged and solve their tasks.

In order to construct such an event trail, web technology uses
cookies, and users can block or remove these cookies from their
browser, therefore granting and revoking access and erasing their
digital footprint. But users are seldom aware that 3rd parties, with
which they may have never interacted, visited and definitely not given
permission to, are also collecting their behavioural data through the
use of so-called 3rd party cookies. And beyond the browser, app
developers collect user data by proprietary means and users have
little ability to control what's being collected nor how it's being
used, or reused, except for some network-centric advertising settings
such as IDFA in Apple's iOS.

It seems that across the board, users do not have enough granular
controls to how their data is being used, nor by whom, and usually the
data arrangements between the service provider and the consumer are
all-or-nothing type of schemes. Given the current state of affairs in
regards to user privacy on the Internet, the hypothesis we are
formulating is that most consumers would like to:

* Have visibility into what events, facts, dimensions and features
  have been collected or inferred about me, anywhere on the Internet,
  i.e. in and by any service provider, across all browsers and
  applications.
* Have feature-level granular controls to grant, revoke and reset
  access to data and information about me, whether they are declared,
  collected or inferred.
* Avoid data and information leakage, i.e. inferred features should
  only be exploitable to those I have granted access to.

## The Application Developers View

Developers need to be able to collect, retrieve, and extract
information out of the user's declared and behavioural data with two
objectives in mind: improving engagement and driving revenue.

In the revenue case, particularly digital advertising, developers will
select technologies that make it easy for the players to adopt and
therefore maximize likelihood of future revenue. For torso and tail
developers the notion of pooling supply to meet the reach and
frequency advertisers require is usually achieved by aggregating
inventory and packaging in SSPs and ad networks, as only a handful of
developers have independently the necessary volume.

In the engagement case, early stage developers want to pool
behavioural data with other developers, and the concept of an external
pool of user declared or activity data they can access becomes
critical since independently they would not be big enough to gain
sufficient insights. In fact, the biggest open pool of data today is
Facebook, via it's Share and Like actions scattered across the web.
Developers give up behavioural signals in exchange for future traffic
in the form of social referrals.

Another concern for developers is the one of not crossing the stream:
users reject ads targeted to them via inference from information they
disclosed in a non-advertising context. Even large players like Google
or Yahoo are cautious not to cross the streams, and when they do,
users revolt, e.g. when using mail data to target ads.

The hypothesis that we are formulating is that developers would like
to:

* Store and retrieve both declared and behavioural data.
* Monetize, with the users consent and adequate controls, for the data
  generated on their sites, possibly advertising but also other means.
* Pool their data with other developers to create more engaging
  experiences, in a model whereby they both control what's been pooled
  as well get additional revenue from other developers leveraging
  their data, hence introducing a data lineage and protection
  requirement.

## The Advertising Players View

Online advertising is a game of predicting response probabilities,
whether that is in display, search, contextual or native, and across
all pricing model, be it in impressions, clicks or conversions.
Advertisers want to maximize the return on their marketing spent, by
reaching the right audience, and/or getting the "correct" clicks that
lead to conversions. But across the board, the key problem is
estimating response probabilities given the historical users'
behaviour. All players (DSP, DMP, SSP, etc.) collect user's data in
order to create response prediction models.

Response prediction probabilities improve with the size of the
training dataset. Although subsampling is an adequate technique,
especially when all positives are preserved and negatives are
subsampled, we know that the estimation bias is smaller when the
training dataset is larger, more so in online learning systems.
Advertising players therefore have a large incentive to get access to
the largest available pool of behavioural data.

Additionally, the latency at which new data gets processed is critical
for applications that have high churn, such as advertising.
Advertising players have a large incentive to reduce the time it takes
them to react to new demand.

The hypothesis is that advertising players would like to:

* Have access to the largest learning capabilities, for the largest
  possible pool of users and with as much behavioural data as
  possible.
* Create their own models to predict probabilities, e.g. clicks and/or
  conversions, to optimize when impressions happen so that campaign
  objectives are met.
* Have models (re-)trained in seconds, not hours.

## Adoption Tactics

The problem of creating a platform is figuring out where to subsidise
adoption to achieve critical mass. Once critical mass is reached,
network effects make the platform self-sustained (it gets adopted
because it works, and it works because it gets adopted). A possible
adoption tactic lies in figuring out where the biggest pain is today.

Although privacy is a problem for users, it's not such a _huge_
problem that will lead them to change online habits, at least
statistically speaking. And without users, there are no advertisers
(and creating demand is a people-intensive and sales-centric process
which does not resonate with a platform business).

That only leaves developers as the initial targets of the platform. To
attract developers, these are possible steps:

* Provide iOS and Android application developers user-based storage,
  similar to what parse.com used to be.
* Provide a minimum schema for event logging, that can then be used to
  do relatively simple learning tasks.
* Give a closed learning platform with simple binary classification,
  based on online logistic regression, to predict most popular X,
  where X can be articles, movies, games, currency, posts, friends,
  etc.

The next step into the platform is to provide users with granular
controls:

* All facts (events and features) are encrypted.
* All facts have lineage to the source (for now).

Finally, the last step is to onboard advertising players:

* Advertising players can train their own online logistic regression
  and random forest learning models, against the available data.
  Models are encrypted.
* Models operating on the data are encrypted and can only access and
  produce the facts for which they signed for (through the equivalent
  of a model certificate authority).
* All facts carry lineage to players involved in the generation or
  aggregation of such fact. Such lineage is visible and can be
  controlled by the user.

There is an alternative adoption tactic, more labour intensive, by
on-boarding existing ad tech players that generate events, e.g. mobile
SSPs, etc. However, this feels more risky due to the longer sales
cycle.

## Pricing Schemes

The key idea is to price facts as events, be it raw events or inferred
events, in an open spot market for events. Facts can be published, by
developers and advertisers, and consumed, again by developers or
advertisers.

For example, an ad network will log a click event, which will get used
by a DMP to create a click prediction model, which a DSP will use to
bid on a CPC auction an ad exchange. The raw click could be priced at
$0.0001, but the final bid on $0.24 max CPC could have been only
possible via the intermediaries. The DSP will take perhaps a 10%
commission, of $0.02 per click in this case, which might go $0.005 to
the DMP, etc. Note however that the data lineage is used for control
purposes, by the user and the publisher of the fact. The pricing only
reflects the value of the "intelligence" added on top, e.g. a logistic
regression model calculating the probability of click being the
intelligence added on top of the raw impression and click events.

Consumers may decide to multi-plex events, and re-publish to allow
multiple consumers upstream, e.g. a DMP might feed multiple DSPs. The
assumption is that the market will be price efficient and information
exclusivity will be priced higher than commoditized information, so an
equilibrium will be met that maximizes the total information welfare.

NB: what this is saying is that BlueKai has a market incentive to only
do business with the largest media buyers, and that by selling data to
more players BlueKai is actually eroding their own pricing and total
revenue.

## Swarms of Intelligence

An evolution of the marketplace, particularly interesting for users,
but also to reduce computational costs, is to leverage device storage
and computation power.

Whereas the learning phases require access to as much data as
possible, the scoring or inference test) only requires a particular
instance or record of the data and the model. This allows for keeping
the user data always on-device, perhaps synchronized across devices,
and having the trained models be encrypted be shipped to the phone,
where the scoring happens. The device would then call the model
service provider with the outcome of the scoring. Service providers
wanting to access the user activity need their algorithms to be signed
by a "user data certificate authority".

## Genomics

One final extension could be to apply the technology to Genomics,
allowing users to control the privacy around their sequencing,
granting selective and limited access to service providers in order to
avoid data leakage.
