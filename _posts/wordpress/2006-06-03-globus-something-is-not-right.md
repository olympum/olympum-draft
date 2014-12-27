---
layout: post
title: Globus, something is not right
date: 2006-06-03 18:12:00.000000000 +01:00
categories:
- Architecture
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409283645063168'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I was reading yesterday the tutorial for the Globus Toolkit 4 (<a href="http://www.globus.org/toolkit/">GT4</a>), especifically <a href="http://gdp.globus.org/gt4-tutorial/multiplehtml/ch03s01.html">this</a> and <a href="http://gdp.globus.org/gt4-tutorial/multiplehtml/ch03s02.html">this</a> page. It highly disturbs me. Something is not right. It reminds me of the CORBA, and early day's of EJBs. 90% systems programming, for 10% application programming. Thankfully AOP, Spring, Hibernate and friends kicked in to help, and introduced Inversion of Control to the masses. Hollywood's principle for everybody.

<p>In GT4, you code manually the WSDL, and your Java classes reference directly the framework and XSD namespaces.</p>
<p>I believe writing the WSDL/XSD by hand is a good thing when you are writing truely reusable (web) services, to ensure they are not just doing RPC over a pretty crappy protocol, and you are focusing on the message. However, if Globus is to be used for parallel computing, ala my beloved <a href="http://www.csm.ornl.gov/pvm/">PVM</a>, you actually want RPC-style, and Globus should be generating the WSDL automatically upon deployment without developer's intervention.</p>
<p>Additionally, when it comes to the Java side, the code looks like an EJB in the 90s. I don't care if you could generate that code, it simply sucks as a class.</p>
<p>I look forward to the Spring of GT4 to come out really soon!</p>
