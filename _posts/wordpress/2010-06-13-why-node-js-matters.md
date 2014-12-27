---
layout: post
title: Why node.js Matters
date: 2010-06-13 15:36:30.000000000 +01:00
categories:
- Internet
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409154158497792'
  _wpcom_is_markdown: '1'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

Since the days when I coded my first reactor [POSA2] back at MIT, I have been convinced of the
conceptual simplicity of non-blocking event driven server. Aside not blocking for I/O and being able
to scale well beyond polling architectures, it is harder, sometimes impossible, to make concurrent
programming mistakes with an event-driven programming paradigm. However, reactor servers never took
off massively, probably because event based programming of server-side applications is a more
complex programming paradigm for the average programmer than a thread- or process-per-request. In in
a way, we have had not enough pressure to move, yet. Things would just work, reasonable well.

<p>But I believe we are finally at a turning point. Multi-core architectures imply <a href="http://www.olympum.com/future/composable-and-concurrent/">the end of the free
lunch</a>. It is happening. Writing highly
concurrent server-side applications that are able to scale linearly as the number of cores increases
is something that we should be preparing for.</p>
<p>Once you believe reactor servers are the future, and somewhat the present, comes the question of
programming language. When it comes to programming for the web, there are many religions and
options: PHP, Ruby, Python, Java, C#, ... However, when it comes to writing web applications, there
are three languages on which all web developers agree universally on: HTML, CSS and Javascript.</p>
<p>And this is what makes node.js exciting. node.js develops a reactor server on top of Google's V8
Javascript engine. First, it solves the free lunch problem using a language that is universally
accessible to web developers. Second, it opens the door for innovation to a world of extremely high
concurrency, for example, MMORPGs, and potentially to a completely different web interaction
paradigm.</p>
<p>With motivation in mind, I set myself to learn a bit more about node.js. I chose one possible stack,
node.js + express + mongodb, but there are many more to learn. What follows in the rest of this post
are my raw notes, which I am posting here just in case it helps fellow developers getting up to
speed in all this new cool technology.</p>
<h2>Installation</h2>
<p>First, we install <a href="http://nodejs.org/">node.js</a> itself, and <a href="http://github.com/drnic/kiwi">kiwi</a>, a
packaging system for node.js, using homebrew (I have dropped Macports in favor of
<a href="http://github.com/webs/homebrew">homebrew</a>, as it allows me to create my own installation recipes
really easily).</p>
<pre><code>$ brew install node
$ brew install kiwi
</code></pre>
<p>That installed for me:</p>
<pre><code>kiwi (0.3.1)
node (0.1.98)
</code></pre>
<p>Once we have kiwi, we install the <a href="http://expressjs.com/">express</a> framework:</p>
<pre><code>$ kiwi -v install express
</code></pre>
<p>Finally, we install <a href="http://www.mongodb.org/">mongodb</a>:</p>
<pre><code>$ brew install mongodb

If this is your first install, automatically load on login with:
    cp /usr/local/Cellar/mongodb/1.4.3-x86_64/org.mongodb.mongod.plist ~/Library/LaunchAgents
    launchctl load -w ~/Library/LaunchAgents/org.mongodb.mongod.plist

If this is an upgrade and you already have the org.mongodb.mongod.plist loaded:
    launchctl unload -w ~/Library/LaunchAgents/org.mongodb.mongod.plist
    cp /usr/local/Cellar/mongodb/1.4.3-x86_64/org.mongodb.mongod.plist ~/Library/LaunchAgents
    launchctl load -w ~/Library/LaunchAgents/org.mongodb.mongod.plist

Or start it manually:
    mongod run --config /usr/local/Cellar/mongodb/1.4.3-x86_64/mongod.conf
</code></pre>
<p>And finally, the native adapter to mongodb for node.js:</p>
<pre><code>$ kiwi install mongodb-native
</code></pre>
<h2>Hello World</h2>
<p>Fire text editor and create app.js:</p>
<pre><code>var kiwi = require('kiwi')
kiwi.require('express')

get('/', function(){
  this.contentType('html')
  return '&lt;h1&gt;Welcome To Express&lt;/h1&gt;'
})

run()
</code></pre>
<p>And back to the terminal:</p>
<pre><code>$ node app.js
</code></pre>
<p>Point the browser to:</p>
<pre><code>http://localhost:3000/
</code></pre>
<h2>Tutorial App</h2>
<p>I found a good blog with many <a href="http://howtonode.org/">node.js tutorials</a>, including one on building
a <a href="http://howtonode.org/express-mongodb">blog app example</a> that included <a href="http://github.com/creationix/howtonode.org/blob/master/articles/express-mongodb/express-mongodb-2.zip">source
code</a>
using express and mongodb.</p>
<p>To run the demo, first start mongodb, and then node.js (I used two terminal windows):</p>
<pre><code>$ mongod run --config /usr/local/Cellar/mongodb/1.4.3-x86_64/mongod.conf
$ node app.js
</code></pre>
<p>And then visit <code>http://localhost:3000/</code>. I could not create a new blog post by visiting
<code>http://localhost:3000/blog/new</code>, as I'd get an error:</p>
<pre><code>/Users/brunofr/Projects/express-mongodb-2/app.js:39
        title: article.title,
                      ^
TypeError: Cannot read property 'title' of undefined
    at /Users/brunofr/Projects/express-mongodb-2/app.js:39:23
</code></pre>
<p>Looking at the code, it seems like the route <code>blog/*</code> is being executed before <code>blog/new</code>:</p>
<pre><code>get('/blog/*', function(id){
  var self = this;
  articleProvider.findById(id, function(error, article) {
    self.render('blog_show.html.haml', {
      locals: {
        title: article.title,
        article:article
      }
    });
  });
});

get('/blog/new', function(){
  this.render('blog_new.html.haml', {
    locals: {
      title: 'New Post'
    }
  });
});
</code></pre>
<p>Reversing the order fixed the problem.</p>
<h2>Benchmark</h2>
<p>I found one interesting benchmark, on <a href="http://tjholowaychuk.com/post/543953703/express-vs-sinatra-benchmarks">Express vs
sinatra</a>, which as always
should be taken with a grain of salt. But the benchmark illustrates some of the properties of
reactor servers that we have been talking about.</p>
