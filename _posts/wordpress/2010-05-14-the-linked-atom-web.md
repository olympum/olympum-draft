---
layout: post
title: The Linked-Atom Web
date: 2010-05-14 05:02:08.000000000 +01:00
categories:
- Internet
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409157174595584'
  _wpcom_is_markdown: '1'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

The release of Facebook's Open Graph Protocol has spurred renewed interest
in the semantic web. I give credit to Facebook for pushing forward an RDFa
derived format onto the world wide web. In fact, RDFa is the least
interesting part. Producing semantic data has been around for a long time.
Most importantly, I give Facebook credit for focusing on the interesting
part of the problem: consumption of semantic data.

<p>And although it's a great achievement, I regret the locked-in and
centralized nature of Facebook's Open Graph Protocol. The web is an open
environment, where open wins at the end.</p>
<h2>Entity Identifiers</h2>
<p>Facebook assigns and owns internal identifiers to entities. These
identifiers do not look unique, nor something that external parties,
disconnected from Facebook could assign, inspect or do anything useful with.
By owning the identifiers, Facebook is owning the entity graph.</p>
<p>The assumption of a single party owning the identifiers for entities is
fundamentally flawed. Entities appear, disappear, merge and fork. Known
entities change constantly, and most importantly what you and I, or anybody
else understands and knows as an entity is different. IMDB and Netflix will
both describe the movie "The Book of Eli", however each use different
identifiers. To assume that one unique identifier can be used consistently
and universally across the web leads to information lock-in.</p>
<p>Luckily, the web is an open environment. And, at the end, open wins on the
web (prove by induction to the avid reader).</p>
<p>Identity on the open web is federated, starting at the top-level domain
identifiers, and all the web to a fully qualified Universal Resource
Identifiers (URIs). In reality, there are many sources of truth. Some of
those are canonical, or trusted, yet many other sources exist. Movies data
from IMDB or Netflix will usually be considered canonical. Yet that does not
stop Wikipedia, or any web publisher, from creating its own entities. All it
takes is a URI.</p>
<p>Anybody on the web, be it Facebook or Freebase, can make statements such as:
this URI on Netflix is about the same movie as this other URI on IMDB. All
it takes is a web page with a couple of links. The difference between
Facebook and the "web" way, is that a web page is identified by a URI, and
anybody can create one in a federated way. Not just Facebook.</p>
<h2>Semantic Web Annotation Techniques</h2>
<p>The most interesting value of the web is not about describing resources, or
the roles of the relationships between resources, but the relationships
themselves. The statement "Madonna is related to Guy Ritchie" is, in
relative terms, more important than the more fact-complete "Madonna is Guy
Ritchie's ex-wife". Although the fact "ex-wife" increases knowledge, it has
only value once we asserted that the relationship exists. Establishing
relationships can be achieved through links and URIs. That's what the web is
about. Pages and links to other pages.</p>
<p>The problem however with the current web of pages and links is that all URIs
are anonymous. Ideally, I would like to bring some structure to those
relationships so that I can codify exactly what "ex-wife" means. That's what
semantic annotations address: naming the role in the relationship between
resources in a structured format.</p>
<p>Inlined semantic annotations, ala Facebook, is one possible way of linking
data sets. The issue however with this approach is that the meta-data about
the resource is mingled with the data. This creates a number of problems.
First, there is an arbitrary distinction between what constitutes data and
what is metadata. Additionally, one needs to be able to parse the resource
format in order to find the semantic annotations. Aside the parsing
computing cost, adding semantic annotations to videos, images, etc. would
require custom extensions to be container format, which is practically
unfeasible. Practically speaking inline semantic annotations are only
partially useful, and only for text-readable content types.</p>
<p>A better alternative would be to use out-of-line semantic annotations. In
this model, we cleanly separate meta-data from the resource data itself.
This separation should be not just syntactical, but structural. Semantic
annotation constructs should treat the data as an opaque resource. For all
we care, we should treat all data as binary resources. If we wanted to look
into the data, an specialized parser would read the data, and surface
interesting facts that we could then promote to metadata.</p>
<p>The first possible construct that provides out-of-line semantic annotations
is the <a href="http://tools.ietf.org/html/draft-nottingham-http-link-header-10">Link HTTP
Header</a>.
Using link headers we can describe a web resource without having to parse
the payload, by simply looking at the HTTP headers. Examples of usage for
link headers could include:</p>
<pre><code>  Link: &lt;http://www.cern.ch/TheBook/chapter2&gt;; rel="Previous"
  Link: &lt;mailto:timbl@w3.org&gt;; rev="Made"; title="Tim Berners-Lee"
</code></pre>
<p>Although powerful, link headers are not particularly accessible for most
publishers, since they require programming access to the web server to
generate those link headers. Additionally, if we are only interested in the
semantic annotations, fetching a full document only to throw it away is
highly inefficient both for consumer and publisher.</p>
<p>A better construct to provide out-of-line semantic annotations is to create
a separate resource altogether representing the semantic annotations for the
parent resource. This alternative, alike link headers, also differentiates
between data and meta-data, but does not require stack changes to HTTP.
Furthermore, it does not require the publisher to generate those semantic
annotations. Anybody can publish semantic annotation documents for any
resource on the web. In that sense, the use of out-of-line semantic
documents that describe web resources is truly open and federated.</p>
<h2>The Linked-Atom</h2>
<p>There are many possible formats for describing resources in an out-of-line
fashions. One of the most interesting formats ones is the <a href="http://www.ietf.org/rfc/rfc4287.txt">The Atom
Publishing Format</a>. With Atom, the
focus is on identity and linking resources. The actual content is hidden
away.</p>
<p>But within the context of semantic annotations, Atom has its
<a href="http://www.olympum.com/future/a-web-linked-by-atoms/">shortcomings</a>. Rather
than abusing Atom, perhaps we need to create a separate, specialized
out-of-line resource descriptor. I call such format the "Linked-Atom". There
are a few differences between Atoms and Linked-Atoms. Whereas the atom is a
generic format for content publishing, the linked-atom is only using for
linking web resources.</p>
<p>Let's consider a graph whereby:</p>
<ul>
<li>Each resource on the web is unique identified by a URI. Let's make such
resource a vertex, and the identity of this vertex be the URI.</li>
<li>A resource can link to other resources, also identified by URIs. We'll
make each link a directed edge, and the link's identity the URI of the
target resource.</li>
<li>Edges have a type, which corresponds to the type of the target resource.</li>
<li>Edges might be named, or remain anonymous.</li>
</ul>
<p>In this graph, the set of a vertex and its outbound edges constitutes a
linked-atom. The linked-atom introduces some additional constraints:</p>
<ul>
<li>A linked-atom is immutable. A change in the graph (adding or removing
edges, or changing edge types or edge names) creates a new Atom, with the
vertex identifier and a new revision number.</li>
<li>Linked-atoms are identified by a composite key composed of the vertex
identifier and the revision identifier.</li>
<li>The list of all linked-atoms describing all revisions of a vertex
constitutes a collection.</li>
<li>Collections are uniquely identified by the vertex identifier.</li>
</ul>
<p>A possible JSON representation for a linked-atom would be:</p>
<pre><code>    {
        "id": "http://example.com/foo.html",
        "rev_id": 1,
        "links": [
            {
                "id": "http://example.com/bar.html",
                "rev_id": 2,
                "type": "text/html",
                "name": "bar" 
            },
            {
                "id": "http://example.com/toto.png",
                "rev_id": 1,
                "type": "image/png",
                "name": "toto" 
            }
        ] 
    }
</code></pre>
<p>A more compact representation of the atom is perhaps more interesting for
extracting information. Instead of grouping all the edges into a single
document, we would create describe each vertex-edge relationship as a
N-tuple. A possible implementation of the linked-atom could use n-tuples to
store the data:</p>
<pre><code>    http://example.com/foo.html 1 http://example.com/bar.html 2 text/html bar
    http://example.com/foo.html 1 http://example.com/toto.png 1 image/png toto
</code></pre>
<h2>The Graph</h2>
<p>Using linked-atoms, we can model the information in the web, not simply as a
graph of pages and links, but a graph of named and typed links between
vertices. Each linked-atom represents a statement about a web resource, a
piece of knowledge. The advantage of a linked-atom graph is that anybody can
publish a document making statements via linked-atoms and collections of
linked-atoms, and not just the publisher of the web resource.</p>
<p>This is in contrast with Facebook's Open Graph Protocol, where only the
publisher of the web resource can make such statements, and where only one
consumer assigns identifiers to those statements. Maybe the Linked-Atom is
not the perfect construct, but it provides an alternative to what I see as a
centralized lock-in model that threatens the open nature of the web.</p>
