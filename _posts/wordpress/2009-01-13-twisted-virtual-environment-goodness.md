---
layout: post
title: Twisted Virtual Environment Goodness
date: 2009-01-13 14:35:09.000000000 +00:00
categories:
- IMPS
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409185468977153'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415059678;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:121;}i:1;a:1:{s:2:"id";i:36;}i:2;a:1:{s:2:"id";i:118;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

Python 2.5.1 is bundled into Mac OS X 10.5 (Leopard), which comes also with setuptools. The breadth of easy_install packages is available pretty much at your fingertips on Leopard.

<p>On the downside, Leopard’s python ships with old versions of some packages, and we might need to upgrade them. We are left with three choices:</p>
<ol>
<li>Overwrite packages with new ones.</li>
<li>Install new ones and set PythonPath.</li>
<li>Use virtualenv.</li>
</ol>
<p>I prefer to use #3. It’s cleaner, it does not change my system, it allows as many environments as we like without one contaminating the other, while at the same time not requiring a fresh python re-install for every working environment.</p>
<p>I want to create an environment for my imps-to-xmpp gateway, for which will be using twisted words. I want to use the latest version (8.2), but the shipped version with leopard is fairly old (2.5):</p>
<pre><code>$ which twistd
/usr/bin/twistd
$ twistd --version
twistd (the Twisted daemon) 2.5.0
Copyright (c) 2001-2006 Twisted Matrix Laboratories.
See LICENSE for details.
</code></pre>
<p>So, we’ll start by installing virtualenv using setuptools:</p>
<pre><code>$ easy_install virtualenv
</code></pre>
<p>And now, we’ll create a virtual environment on which we can install the updated twisted:</p>
<pre><code>$ cd ~/Sites/
$ mkdir python
$ cd python
$ virtualenv imps
$ source imps/bin/activate
$ easy_install twisted
</code></pre>
<p>We can now check that we are running the latest version of twisted (8.2 as of writing):</p>
<pre><code>$ twistd --version
twistd (the Twisted daemon) 8.2.0
Copyright (c) 2001-2008 Twisted Matrix Laboratories.
See LICENSE for details.</code></pre>
