---
layout: post
title: Rails, Django, CodeIgniter, Symfony Performance Compared
date: 2007-02-17 09:18:18.000000000 +00:00
categories:
- Frameworks
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409267828748289'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415449672;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:10;}i:1;a:1:{s:2:"id";i:72;}i:2;a:1:{s:2:"id";i:363;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

Surely performance is not the prime criteria for selecting a framework. Most people will say developer productivity, ease of maintenance, security and scalability are the most important factors.

<p>I love the Ruby language and its expresiveness. And Rails has been a truly inspiring web framework. This is why I think the <a href="http://www.alrond.com/en/2007/jan/25/performance-test-of-6-leading-frameworks/">web frameworks performance test results run by Alrond</a> (and an update <a href="http://www.alrond.com/en/2007/feb/04/in-addition-to-the-test-of-mvc-frameworks/">here</a>) are highly disappointing for Rails. In Alrond's tests we find that Django giving up to 4x faster response times, and 2x more throughput. But I guess this is not a surprise, we always knew Python was faster than Ruby by just looking at <a href="http://shootout.alioth.debian.org/gp4/benchmark.php?test=all&amp;lang=python&amp;lang2=ruby">Debian's language shootout</a>.</p>
<p>I would add a couple of remarks to Alrond's results:</p>
<ul>
<li>Most shared web environments only offer PHP. Some hosting providers offer an old version of Python that will not support Django. So when using shared hosting, PHP is likely to be your only choice. PHP is a useful and proven language if you need to integrate with C/Java/whatever, but perhaps not as expressive nor OO as Ruby and Python. On the performance results side of things, CodeIgniter/PHP tests using a bytecode cache (APC) improve performance by 10x, and make them comparable to Django/Python. Plus CI runs on PHP4, which is what most web hosts out there are running today.</li>
<li>If you want/have to avoid PHP, you are probably looking at Rails and Django as your main options. These will require you to use a Virtual Private Host or a dedicated server. Rails and Django don't work well on shared hosting. And if you are like me, on a tight hosting budget, you really want to get that extra performance and be on a framework where it's <em>really</em> cheaper to scale out. This is where Django/Python will shine.</li>
</ul>
<p>At the end of the day, choosing between one of these web frameworks is actually a language choice. And right now, the only real language contestants for people looking for raw speed and stability are PHP (with opcode cache) and Python. And both seem to deliver comparable performance.</p>
<p>But I would not rule out Ruby completely just yet. <a href="http://jruby.codehaus.org/">JRuby</a> is making a lot progress, and you can even now <a href="http://recompile.net/2006/11/how_to_deploy_jruby_on_rails_a.html">run Rails with JRuby in  Sun's JEE container (glassfish)</a>. On the other hand, another interesting similar development which might rock Python is <a href="http://www.codeplex.com/Wiki/View.aspx?ProjectName=IronPython">IronPython</a>, which runs Python on the .NET runtime.</p>
