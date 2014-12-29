---
layout: essay
published: true
author: Bruno Fernandez-Ruiz
title: The Datastream Marketplace
subtitle: A Reverse Auction Mechanism for Algorithms
date: 2014-12-29
---


## Decision Automation

We are currently seeing how data processing needs are exploding.
Consumers are leaving a growing crumb trail of events as they use the
Internet. Sensor-data telemetry is growing into the trillions of
machine-generated events per day. DNA sequencing is generating
terascale genome databases, per human being. On top of generating and
collecting more data, the expectations as of how the data is used are
also growing.
 
Social data platforms, such as Foursquare or Twitter, have educated
consumers about seamless data manipulation, in exploratory,
unstructured and close to real-time ways. Businesses owners now expect
similar flexibility in the analysis of inventory, catalogue and
procurement data, joining their proprietary data with open data sets.
The objective is to make better and faster business decisions. Just
like businesses, individuals are also using data mashup capabilities
to make better informed decisions when buying a house, selecting
utility providers, changing insurance, etc.

Advertising exchanges, stock exchanges, energy exchanges, etc. see
billions of daily automated trades, which computers make by processing
large amounts of data using advanced mathematic models, e.g.
segmentation, targeting, pricing, risk, sizing, etc. But outside these
exchanes, only a few data technology powerhouses have today the
infrastructure, skills, distribution and algorithmic bench to
implement analytics, prediction and forecasting at terascale.

The basic **technology infrastructure** required to compute and solve
big data problems, especially when real-time answers are needed, is
very nascent. A few successful big data technology infrastructure
pioneers like Splunk are opening the way. But we are still very early
in the cycle and the skills necessary to solve big data problems are
hard to find. Because of the lack of viable and easy to use technology
solutions, research in scaling **machine learning** to big data
problems has been very limited.

So far, we have seen big data solutions put most emphasis on
analytics, i.e. answering questions for humans to make decisions.
Little effort has been spent in using big data to dynamically change
business processes through predictions and **decision automation**.

We need to create a **business intelligence decision automation
platform** where the next Industrial Internet Revolution[^ge] can
happen. In this platform, machine- and human-generated data will be
captured, collected and distributed at terascale, and immediately
processed for analysis, estimation, prediction, forecasting and
anomaly detection using highly scalable A.I. techniques. This will
enable a revolution around decision automation, across agriculture,
industry and services, and a new **data marketplace** pivoted on the
intelligence / decisions inferred out of data.

[^ge]: The _Industrial Internet_ is a term coined by General Electric, somewhat close to what Kevin Ashton called the _Internet of Things_. I prefer to use GE's term, as it speaks more to the intelligence and the revolutionary decision automation implications that machine learning and big data will have on the industry, unlike IoT which talks more about connecting physical things to the Internet and the resulting sensor-data generation, but speaks less to the decision automation factors. In fact, one could argue that there is also an _Internet of Humans_, an _Agricultural Internet_, ... so perhaps we are missing a new and more encompassing term.

## Decision Platform Capabilities

The Business Intelligence Decision Automation Platform (BIDAP) is two
things: a technology platform and a marketplace. Technically, BIDAP
provides a distribution and computation framework; distributed online
learning; and provenance and leakage control. In addition, BIDAP is
also a big data marketplace where application developers sell
(publish) or buy (consume) events from datastreams in an auction. The
bid is truthful to the value derived out of the event.

Out of the components of BIDAP, the marketplace is the business
keystone. In other words, this is not a venture to create and sell a
technology platform offering distributed learning on datastreams.
Although the technology is a large part of the innovation required, we
are not selling technology. In fact, the expectation is to build as
little core infrastructure as possible, and to reuse existing
technology and distributed machine learning frameworks as much as
possible.

### Datastreams on the Cloud

We are at the right point on time when this platform can be created.
Pretty much up to now datasets were physically split and stored
on-premise. Data owners wanted to keep their proprietary assets
physically controlled. But cloud infrastructure and Hadoop have opened
the way for startups to keep all their data on the cloud. Most
importantly, sensor-devices are completely shifting data to the cloud
and away from on-premise. Many datasets now just flow continuously
into Amazon Web Services (albeit, they are still not joined, but at
least they are "physically close").

### Trading Instruments

Marketplaces around data are not new. Several types of data
marketplaces exist already:

* Static dataset licensing, e.g. Infochimps, twitter's firehose,
  Bloomberg, etc. These are not efficient, since there is limited
  transparency and almost no liquidity as one must buy a time-bound
  license to the datastream up-front.
* Data Management Platforms (DMP) in online advertising, e.g. BlueKai,
  and data clearing houses, e.g. Acxiom. Both are highly succesful
  businesses that operate on batch windows, providing qualified
  audience segment scoring lists. Their revenues depend on very
  difficult attribution calculations based on how well those audience
  segments perform compared to others not using the data. To solve the
  complexity of revenue attribution, these companies operate by taking
  a revenue share on the data consuming business.
* Ad exchanges, which operate on a per impression basis. Search,
  contextual and display ad exchanges run an auction, where the
  opportunity is the impression. They are all highly efficient and
  profitable.

An efficient data marketplace must allow spot trades at the lowest
possible granularity, as this increases the number of trading
opportunities (just like in ad exchanges). In a datastreams
marketplace, application developers buy the ability to consume and
compute individual events datastreams.

Trading on events in a datastream is not the only possible model.
Microsoft is trying to create a marketplace where databases on Azure's
SQLServer cloud are the trading instrument. The database as trading
instrument has less liquidity potential than the datastream, and
therefore is less likely to become efficient in the long run.

## e-Sourcing Continuous Decisions

Deploy a fairly standard technology stack in a number of nodes,
on-premise, that can consume the sensor-device datastream that is
proprietary to the customer, and host custom logic to process events
and produce "intelligence". The idea is to then offer the events and a
problem (as a component in a supply chain) to external teams. Each
external team would use their algorithmic bench to infer a solution to
the problem. The producer of the datastream feeds events into the
multiple teams competing, they produce some intelligence and that
intelligence gets fed consumed back by the producer of the datastream.
In reality, it could be that the role of the producer and consumer are
clearly defined and separate. What matters most is that the problem is
clearly defined, with specified input and outputs.

Imagine then two customers that have deployed this platform
on-premise, and that there is an opportunity to join their data to
provide value-add. The data could flow direct between customers, or
through a clearing house cluster on the cloud.

Each solution to the problem will have a different "quality score". We
want the payout to be conditioned by the quality score and the bid
that the intelligence team is willing to sell for. This is an auction
with multiple sellers and one buyer (reverse auction or procurement
auction). Each intelligence offer gets a rank \\(r = bid / quality\\),
and the offer with the lowest rank wins. The buyer can set a maximum
reserve price (auction ceiling). We will have \\(r_1 = b_1 / q_1\\)
and \\(r_2 = b_2 / q_2\\), and \\(r_1 < r_2\\), in an auction where
bidder 1 wins. Then the payout should be such that the seller collects
as much as possible:

\\[p / q_1 \le b_2/q_2\\]

which means that the final payout is:

\\[p = b_2 \cdot \frac{q_1}{q_2} - \epsilon\\]

where \\(\epsilon\\) is the smallest unit of currency allowed in the
trade, e.g. USD 0.01 or USD 1.00 or USD 1,000, ...

The issue around pricing is then determining quality in a transparent
and truthful way. One possibility is for the marketplace operator
being the one determining the quality, but that makes it harder to
sell the solution. The problem is that the quality is measured _after_
taking the decision based on the intelligence provided, comparing the
observed outcome with the predicted outcome.

The question then is who should take the risk for the estimation bias.
The operator? The buyer? The seller?

Imagine in MB that multiple labs teams would compete, per impression.
They would each be providing an ad with a predicted CTR. The team with
the higest predicted CTR would win the auction and get impression. If
the impression translates into a click, all parties are happy. If the
actual CTR is lower than the estimated CTR (over-estimation), then the
seller lab team got too many (unfair) opportunities, and the buyer
incurs a loss. If the actual CTR is higher than the estimated CTR
(under-estimation), then the seller lab team sold too low.
