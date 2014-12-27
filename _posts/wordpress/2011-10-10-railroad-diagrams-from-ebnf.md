---
layout: post
title: Railroad Diagrams from EBNF
date: 2011-10-10 21:04:33.000000000 +01:00
categories:
- Future
tags: []
status: publish
type: post
published: true
meta:
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415524839;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:355;}i:1;a:1:{s:2:"id";i:10;}i:2;a:1:{s:2:"id";i:75;}}}}
  tmac_last_id: '531409136601534466'
  _wpcom_is_markdown: '1'
  _edit_last: '1'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I am playing with a new query language. I am defining the grammar as EBNF, but
I want to show railroad diagrams for those readers that are more graphical and
less familiar with BNF. I've found limited support for generating syntax
diagrams from EBNF.

I've found a few tools, some working better than others:

<ul>
<li><a href="http://www.informatik.uni-freiburg.de/~thiemann/haskell/ebnf2ps/">Ebnf2ps</a>
(Haskell). This is the only tool I have not been able to get to work. I seem
to be missing AFM fonts in my TeX installation and I am not sure I want to
spend time figuring out how to generate the AFM files.</li>
<li>SQLite <a href="http://www.sqlite.org/docsrc/doc/tip/art/syntax/bubble-generator.tcl?mimetype=text/plain">bubble generator</a>
(Tk/Tcl). Strictly this tool does not consume EBNF grammars, but a custom
DSL. If I didn't care about EBNF, this would be the best tool</li>
<li><a href="https://github.com/featurist/node-ebnf-diagram">node-ebnf-diagram</a>
(Javascript). Although it works, I have to issues with it. One is that it
can only generate PNG files. That would not be too bad if it weren't for the
second issue: the tool does not automatically resize the canvas, and it
requires explicit width and height input. If I don't find anything else,
I'll probably end up using it.</li>
<li><a href="http://www.emacswiki.org/emacs/EbnfToPsPackage">ebnf2ps.el</a> (Emacs Lisp).
It works as advertised. The only issue I found is that the diagrams
generated have a small white gap on the lines on the right hand side.</li>
<li><a href="http://www.antlr.org/download.html">ANTLRWorks</a> (Java). Bundled with antlr,
it fits the task. Once you are in the game of defining the grammar in Java,
why not just go ahead and use the same tool to generate not only the parser
but the diagrams? This is what the tool does. Even if you are not doing a
Java parser/lexer, this is a good tool to use for documentation purposes.</li>
</ul>
<p>I am using ANTLRWorks, generating all the diagrams from the command line as part of my markdown transform pipeline:

{% highlight bash %}
java -cp antlrworks-1.1.4.jar org.antlr.works.Console -f yql.g -o output/ -sd eps
{% endhighlight %}

<p>It works very well.
