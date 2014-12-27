---
layout: post
title: Facebook BigPipe in an Async Servlet
date: 2010-07-14 06:44:48.000000000 +01:00
categories:
- Java
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409148978528258'
  _wpcom_is_markdown: '1'
  _edit_last: '1'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415314715;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:315;}i:1;a:1:{s:2:"id";i:313;}i:2;a:1:{s:2:"id";i:335;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

Since <a href="http://www.subbu.org/">Subbu</a> wrote <a href="http://www.subbu.org/blog/2010/07/bigpipe-done-in-node-js">BigPipe using node.js</a>, I had to see how the same thing would look like in a Java async servlet.

<a href="http://codemonkeyism.com/">Stephan Schmidt</a> had already written <a href="http://codemonkeyism.com/facebook-bigpipe-java/">Facebook BigPipe for Java</a>, but using a synchronous servlet model, not asynchronous. I decided to implement it using Jetty continuations and the Jetty HTTP client, but the code should be easy to adapt to servlet 3.0 <code>AsyncContext</code>.

<script src="http://gist.github.com/475077.js"></script>

The code initially constructs the page with a few empty <code>div</code>s that will contain the pagelets, for example:

{% highlight html %}
<div id='pagelet3'></div>
{% endhighlight %}

I keep the connection open from the browser to the server while I render pagelets. As pagelets become available, I flush them onto the browser, which in turn inserts them into the right place in the DOM using Javascript. Assuming we get back a response from the remote module protocol:

{% highlight html %}
<span>some useful message for module: pagelet3</span>
{% endhighlight %}

We wrap it inside Javascript so that it looks like:

{% highlight html %}
<script>arrived('pagelet3', '<span>some useful message for module: pagelet3</span>');</script>
{% endhighlight %}

All is left is for the <code>arrived</code> function to update the
<code>pagelet3</code> element in the DOM. In terms of concurrency, the
initial page construction is done synchronously. As soon as I have the
frame in place with the <code>div</code>s that will eventually hold
the pagelets, I suspend the execution of the servlet, which in turn
releases the thread that was attached to the client connection. At
that point, I fire in parallel HTTP client requests to the remote
module server.

For resuming the continuation, I could have used a counter, but since
each HTTP client execution is a separate thread, unlike in node.js, I
did not want to have to acquire a lock and synchronize to be able to
update the counter. Instead, I used request attributes, as setting,
getting and removing them is thread safe. The code keeps a list of
references to the elements that we are offloading to a remote module
server, as an <code>ArrayList</code> with the ids to fire parallel
requests to <code>http://localhost:8080/module?id={id}</code>; each
<code>id</code> is also kept as a request attribute. As each request
comes back from the remote module server, I write and flush the
response buffer, so that the element appears on the browser
immediately, and I remove the corresponding request attribute.

Although the code is not as readable and straight forward as what
Subbu got with node.js, I am actually surprised how simple the async
Java solution actually turned out to be.
