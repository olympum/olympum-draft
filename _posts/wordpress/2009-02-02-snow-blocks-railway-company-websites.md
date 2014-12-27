---
layout: post
title: Snow blocks railway company websites
date: 2009-02-02 08:11:22.000000000 +00:00
categories:
- Policy
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409168054231041'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415209127;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:316;}i:1;a:1:{s:2:"id";i:118;}i:2;a:1:{s:2:"id";i:324;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

We knew it was coming. Met Office kept talking about. Heavy snow
across the South East of England. Regardless, this morning is a
complete mess, as expected, and the country comes to a halt, as usual.

<p>And to a degree, it is normal. It is very difficult to size transport for peak emergencies. Possible, but costly to the tax payers. So, in a way, I understand we are stuck today.</p>
<p>But what I don't understand is how all the web infrastructure associated with network railways is basically down.</p>
<p>Let's start with Southern Railway:</p>
<p><code><br />
$ curl -v http://www.southernrailway.com/<br />
* About to connect() to www.southernrailway.com port 80 (#0)<br />
*   Trying 213.86.249.117... connected<br />
* Connected to www.southernrailway.com (213.86.249.117) port 80 (#0)<br />
&gt; GET / HTTP/1.1<br />
&gt; User-Agent: curl/7.16.3 (powerpc-apple-darwin9.0) libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3<br />
&gt; Host: www.southernrailway.com<br />
&gt; Accept: */*<br />
&gt;<br />
&lt; HTTP/1.1 500 Generated error<br />
&lt; Date: Mon, 02 Feb 2009 07:57:42 GMT<br />
&lt; Connection: close<br />
&lt; Content-Type: text/html<br />
&lt;<br />
&lt;html&gt;&lt;body&gt;<br />
&lt;h2&gt;No suitable nodes are available to serve your request.&lt;/h2&gt;&lt;/body&gt;&lt;/html&gt;<br />
* Closing connection #0<br />
</code></p>
<p>Okay, so let's see SouthEastern:</p>
<p><code><br />
$ curl -v http://www.southeasternrailway.co.uk/<br />
* About to connect() to www.southeasternrailway.co.uk port 80 (#0)<br />
*   Trying 213.86.249.125... connected<br />
* Connected to www.southeasternrailway.co.uk (213.86.249.125) port 80 (#0)<br />
&gt; GET / HTTP/1.1<br />
&gt; User-Agent: curl/7.16.3 (powerpc-apple-darwin9.0) libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3<br />
&gt; Host: www.southeasternrailway.co.uk<br />
&gt; Accept: */*<br />
&gt;<br />
&lt; HTTP/1.1 500 Generated error<br />
&lt; Date: Mon, 02 Feb 2009 08:04:03 GMT<br />
&lt; Connection: close<br />
&lt; Content-Type: text/html<br />
&lt;<br />
&lt;html&gt;&lt;body&gt;<br />
&lt;h2&gt;No suitable nodes are available to serve your request.&lt;/h2&gt;&lt;/body&gt;&lt;/html&gt;<br />
* Closing connection #0<br />
</code></p>
<p>Not provisioning capacity for an unforeseen event could be excused, but not provisioning capacity for a foreseen event has no excuse, especially for an infrastructure company. This is the core of a public service, and if doing this is not possible, it's time to revisit whether their current hosting arrangements are adequate. Definitely, not impressed, especially when cloud infrastructure is becoming so easily available.</p>
