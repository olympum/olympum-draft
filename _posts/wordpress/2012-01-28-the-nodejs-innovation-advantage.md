---
layout: post
title: The NodeJS Innovation Advantage
date: 2012-01-28 21:40:27.000000000 +00:00
categories:
- Architecture
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409130808819712'
  _wpcom_is_markdown: '1'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415525537;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:315;}i:1;a:1:{s:2:"id";i:245;}i:2;a:1:{s:2:"id";i:251;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

**Thesis**: _"when building large scale distributed systems, high
performance functional programming languages provide the quickest
turnaround from idea to concept; however such advantage disappears as
we move from concept to production, and the overall time from idea to
production across all programming languages is of the same order of
magnitude"_.

<a href="{{ site.baseurl }}/assets/nodejs_innov_advantage.png"><img
src="{{ site.baseurl }}/assets/nodejs_innov_advantage.png" alt="The
NodeJS innovation advantage" title="nodejs_innov_advantage"
width="510" height="366" class="aligncenter size-full wp-image-364"
/></a>

I posted this diagram, without justification, yesterday evening, in
an attempt to gauge the reactions of the community, in <a
href="http://twitter.com/olympum">twitter</a>. Thank you to all of you
that commented. With the experiment done, let me now provide my thesis
and hopefully address most of the feedback so far. I intend to make
this post fluid and keep updating as the conversation evolves.

Now, let me qualify the thesis. First, this is a thesis applicable
to multiple domains, whether that's a low-level network switch
appliance, a http proxy gateway or a web application. As a
consequence, this is not a framework comparison, it's not about Rails
vs Django vs Play vs Express vs .... This is not an argument about
dynamic vs statically typed programming languages, although that
definitely plays a partial role in the thesis.

Mine is a thesis about the complete <em>team</em> productivity by
programming language and across the full product life-cycle from
inception to retirement. The thesis is purely based on my observations
throughout the years. There is not data to back it up, except
anecdotal evidence. In summary, mine is a qualitative statement, not a
quantitative one.

If the thesis were true, this would mean that teams using
high-performance and functional programming languages can iterate more
quickly from idea to concept. Such quick turnaround allows a constant
validation of ideas in the code. Because it is quickly possible to see
the idea running, we can afford to have more ideas. The quicker we are
able to iterate between idea and concept, the more we are
innovating.

Such quick turnaround has a real trade-off and a false
trade-off.

Moving these concepts to production is difficult. Whether it's
Scheme, or Lisp, or Clojure, or JavaScript, it becomes clear that we
are "naked". Except in "safe but useless" languages, such as Haskell,
in most "useful but unsafe" programming languages, the developer has
to compensate for the dynamic nature of the language. The developer
has to provide the <em>strictness</em>, and to a degree perform the
job of the compiler. In statically-typed and imperative programming
languages, the compile infrastructure helps the developer ensure the
correctness of the code. In dynamically-typed and functional
programming languages --by the way, yes these are orthogonal concepts
but usually associated--, the developer needs to structure code and
provide the necessary checks, assertions, unit tests, regressions
tests and modular design. The addition of type hinting and type
inference does not change this, it only shifts effort between "before
concept" and "after concept".

High-performance functional programming languages trade strictness
for innovation potential. Without the additional investment in checks
and tests, these systems are not _predictable_. The time we
gained upfront, we pay later for. I'd argue such trade-off is good,
and allows quick iteration to find the right idea.

The second trade-off is about tech debt. The time to production is
identical across languages, but because the developer in
high-performance functional programming languages had to compensate
for the lack of compiler infrastructure and runtime guardrails by
adding completeness of tests and checks, the system is easier to
maintain and has overall a better architecture. This is almost counter
intuitive and I think most people don't think this way because they
move too quickly from concept to production, and don't implement the
necessary strictness. There is a tendency in the developer to move
quickly from concept to production, and therefore accruing overall
technical debt.

Finally, I believe server-side JavaScript and Google V8 provide
such high-performance functional programming language, in the skin of
an imperative one, and enable this quick turnaround from idea to
concept. This possibly one of the key reasons we are seeing such
explosion in adoption. I only hope developers start to realize the
trade-off they are doing, and that in order to avoid accrual of
technical debt, they better invest in checks and tests before they
rush into production.
