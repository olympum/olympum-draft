---
layout: post
title: A Web Linked by Atoms
date: 2009-03-27 13:14:57.000000000 +00:00
categories:
- Future
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409176887439360'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

Looking back at the past 20 years of the history of the internet, one can realize that what we call today the web has changed dramatically, but that one thing is certain: it will continue to evolve. Gone are the days of manually editorialized directories, of static content, of one way conversations. Today we live in a dynamic, social, interactive web. And it&#8217;s a web that is traversing the digital realm and changing how we understand our physical world, breaking communication barriers and making information and knowledge easily accessible.

<p>Yet, although much has changed, the web remains an almost completely deregulated environment, not only on the legal side, but also on the technical side. That&#8217;s one of the web&#8217;s merits, making it easy to publish documents. Those documents are part of a forest, many sit in isolation, and only a small number of links are connecting those documents. The hyperlink is the web&#8217;s way of connecting documents, yet, because the web is a flexible environment, there are no requirements on developers as of how they structure their documents, nor as what link schemes they use.</p>
<p>But what is an advantage on one end, reducing the barriers of entry to publishers and developers, is also a disadvantage on the other end. We end up with billions of documents that are difficult to navigate, and the information, although there, is difficult to find and access.</p>
<p>Organizing the web has been a growing pain since the early days. As the web evolved, so did the technologies used to organize it. In the beginning, only a few universities and government agencies had documents, and it was feasible to maintain a directory. Later on, commercial entities entered the web at exponential rate, and business were created just to solve exactly this problem: organize the web.</p>
<p>The web is growing so fast, that we are not able to reasonably scale the production and maintenance of web directories. And there came web search engines, based on the information retrieval research of the late 80s and early 90s, to solve this very problem. But search engines are  starting to show their age:</p>
<ul>
<li>We are accustomed to a web that is almost infinite, so deep and wide that we know that not even search engines can reach the very end-leafs of it. We know that the long tail is getting longer, and that the amount of disconnected content is just growing every day.</li>
<li>Traditional media is struggling to find its place in the web social ecosystem. &#8220;Head&#8221; content is expensive to produce, and is becoming less and less profitable to operate. The audience is moving to tail and (social) user generated content, where it spends hours. Media businesses, as we know it, are dying slowly. Content is no longer king, and guess what, search can&#8217;t find the new king.</li>
</ul>
<p>Today&#8217;s problem is also today&#8217;s opportunity. Interestingly, the tools necessary to fix this are <em>almost</em> in place. This the &#8220;Atom Web&#8221;, or a web linked by Atoms, which some would perhaps deem as a bastard child of <a href="http://www.w3.org/DesignIssues/Semantic.html">the semantic web</a>. The Atom Web is a web where the hyperlink is really empowered as the new king, and takes the crown away from content. It&#8217;s a web where document and link meta-data is more important than data, just like the <a href="http://ilpubs.stanford.edu:8090/422/">PageRank algorithm</a> changed search by using link (citation) flows as a measure of relevance.</p>
<p>The <a href="http://www.ietf.org/rfc/rfc4287.txt">Atom Syndication Format</a> and the <a href="http://www.ietf.org/rfc/rfc5023.txt">Atom Publishing Protocol</a> have the capabilities to change the web as we know it, well beyond the initial purpose to serve as a content syndication mechanism. Atom contains almost all the necessary meta-data missing in a HTML document, plus it provides a neat way to link content. But to achieve this, we need to empower Atom by introducing three new principles:</p>
<ul>
<li><em>Content is opaque</em>. We shouldn&#8217;t accept (almost) any extensions to Atom. Atom should be reserved as an envelope containing only meta-data, with the source element containing all the content or a reference to the content resource. Perhaps in a few cases we might need extensions, like search, paging, presence and location. But rather, I see the very large majority of extensions as content.</li>
<li><em>Post Atoms, Get Feeds</em>. Atom entries have little meaning by themselves. Instead, they live in collections through feeds. An entry may belong to many collections. Collections are views, representations, of the underlying documents, grouped in a wide array of combinations. Feeds can represent pretty much anything: the revision history of an entry, all known content about an entity, a blend of categories and topics, related content, etc. Congruent collections are much easier for a UI consumer, as a simple request returns everything necessary to render a widget, a module, or a complete page, perhaps even as JSON directly from the browser. Notice that I am not assigning any semantics to the feed, that&#8217;s up to the implementation, but specifying that a feed is <em>the</em> first class citizen, followed by the entry.</li>
<li><em>Links are type-aware</em>. Links are the most important part of Atom, and content-types are the tools of choice to help bring semantic value to the relations (rather than custom schemas extending Atom). In a way, the Atom Web is a reduced subset, a predecessor, of the Semantic Web, since we don&#8217;t necessarily know the subject-predicate relationship for all structured data (yet). I rather think of something along the lines of <code>&lt;link type="application/atom+xml;content=application/foo+xml"&gt;</code>, which would be describing the content-type inside the referred Atom document. Obviously, you may still point directly to the underlying resource, because you can, and because that&#8217;s how the web works today.</li>
</ul>
<p>Certainly, there is a bit of web infrastructure required to make this true. The same way we have the web server for the sometimes-linked web, we need the atom server for the always-linked web. But an atom server is not just a web server adhering to the the AtomPub protocol. Atom server implementations can provide whichever machinery they want as long as the adhere to the three principles above. An atom server needs to have the ability for publishers to define collections, or more precisely, the matching rules that will define views, and which will be exposed as collections, through feed resources. Such view generation will be offloaded partially to batch computing, perhaps on the form of map/reduce jobs. Some implementations may for example decide to use schema-less document stores in order to generate those views.</p>
<p>One could get started today with this and build a gigantic store replicating copies of the content hosted elsewhere on the web. The store could be populated either by crawling or by allowing developers to publish into it. But eventually, this store would have problems finding all the deep end-leaf documents.</p>
<p>A few big players adopting Atom to expose their data, for example making the webmap available through Atom and opening the API for publishers to post onto the store, could dramatically change this game. There would still be plenty of problems to solve, ranging from the now even more important link-spam detection and moderation, to the not so obvious scaling problems, but at least we would be one step closer to organizing the web.</p>
