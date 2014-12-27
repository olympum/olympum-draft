---
layout: post
title: Pricing Models for Web 2.0 Software as Services
date: 2006-07-30 10:05:00.000000000 +01:00
categories:
- SaaS
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409291278680064'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415197223;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:22;}i:1;a:1:{s:2:"id";i:21;}i:2;a:1:{s:2:"id";i:38;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

The recent advent of Web 2.0 no-software start-ups like <a href="http://www.37signals.com/">37signals</a>, <a href="http://www.salesforce.com/">salesforce.com</a>, <a href="http://www.writely.com/">Writely</a>, etc. is getting plenty of attention by the media and VCs alike, but I have not seem much about the pricing model of these no-software business models.

<p>The basic idea, repeated all over the place in Web 2.0 start-ups, is that one can develop very rich user interfaces using thin client technology. Instead of installing a local copy of Microsoft Word, you use <a href="http://www.writely.com/">Writely</a>. Instead of installing <a href="http://www.siebel.com/">Siebel</a> in your enterprise as a CRM solution, you use <a href="http://www.salesforce.com/">Salesforce.com</a>. And so forth. Even Microsoft's Bill Gates, highly concerned about the future of Microsoft in a world of "applications built from the grassroots" is putting forward an online <a href="http://news.com.com/Microsoft+plans+Live+CRM+service/2100-1011_3-6092503.html">Microsoft Live CRM service</a>.</p>
<p>The advantage of using online solutions are allegedly savings in infrastructure and support costs. But is this really true?  Will individuals and business of all sizes alike chose online services versus an offline dedicated solutions? Obviously not, so who is then the target customer? Or rather, when will a consumer chose online vs offline applications?</p>
<p>An informed consumer (be it a home user, a web designer, or a CIO) will make a choice based on the expected utility he gets as a consumer from the software. He will compare the utilities and chose the one that seems most likely to suit his needs. The expected utility for each option, online or offline, will surely include quantifiable factors, such as software price, downtime costs, support costs, infrastructure costs, etc. as well as perceptions such as privacy, reputation, etc.</p>
<p>I prepared a highly simplified <a href="http://elsa.berkeley.edu/%7Emcfadden/">utility model</a>  that I could use to bring some light. In this model the only factors I considered were:</p>
<ul>
<li>Software price, for an offline solution, expressed as a monthly depreciation cost as a function of the number of employees. For solutions that require systems integration and professional services, I have diluted the cost of consulting in the total price of the solution, which then gets expressed as part of the monthly depreciation costs per employee.</li>
<li>Service price, as a monthly recurring charge by the provider as a function of headcount.</li>
<li>Infrastructure costs, for the offline solution, usually comprising storage, servers, backup, etc.</li>
<li>Service support costs for the offline solution, to support the local infrastructure costs.</li>
<li>Cost of downtime. I have assumed local class 4 availability in each domain. This translated into 0.01% downtime for offline software, 0.01% to local network, 0.01% to the local ISP, 0.01% to the provider ISP, and 0.01% to the service itself.</li>
</ul>
<p>I have run the model with existing data for both "consumer applications", using 37signals <a href="http://www.basecamphq.com/">Basecamp</a> and Microsoft Project for pricing data, and for "enterprise applications", using Siebel and Salesforce.com for pricing.</p>
<p>The model yields interesting results:</p>
<ul>
<li>For both consumer and enterprise applications, the break-even point where the software-as-a-service is not competitive anymore is somewhere around 500 employees.</li>
<li>The key differentiation between the utilities derives from infrastructure and support costs. For small to medium businesses, the cost of a dedicated and under-utilized infrastructure and service support personnel is prohibitive, and only large companies are able to realize economies of scale to make offline support viable.</li>
</ul>
<p>We can clearly see the validity then of these start-ups, since in <a href="http://www.census.gov/csd/susb/susb03.htm">2003</a>, there were 5.7 million businesses in the US with less than 500 employees, at an average of 10 employees per firm; and 16,926 businesses with more than 500 employees, at an average of 3,300 employees per firm.</p>
<p>These 57 million businesses with 10 employees cannot afford the costs of dedicated infrastructure and service support, and are better off to chose an online application. For an average of 10 employees per firm, the model yields a cost of approximately $5,000/month for an offline solution, versus a $150/month for an online solution. $4,850/month of infrastructure and support savings surely justify the consumers choice.</p>
<p>As a side effect, the model yields a potential market size of approximately $10 billion for the Office applications, possibly close to $50 billion for the standard applications used currently in small and medium-sized businesses.</p>
<p>To conclude, it's interesting to note that the online software-as-a-service business model is a side-effect of an underlying consumer pain: lack of secure shared infrastructure.</p>
