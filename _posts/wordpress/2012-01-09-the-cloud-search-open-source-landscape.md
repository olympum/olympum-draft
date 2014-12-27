---
layout: post
title: The Cloud Search Open Source Landscape
date: 2012-01-09 07:23:20.000000000 +00:00
categories:
- Architecture
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

At some point in the race of scaling a search application, as query
load (queries per second) and corpus size (number of documents)
increase, we need to distribute things. Distribution means in
practical terms sharding the index, and we need to solve both
**distributing indexing** as well as **distributed search**.

To achieve **distributed indexing** we may either shard by document or
shard by term:

1. Document-based sharding: each shard has index for subset of docs. A
   K word query requires O(K*N) disk seeks on N shards.
1. Term-based sharding: each shard has subset of terms for all docs. A
   K word query requires O(K) disk seeks, but much higher network
   bandwidth is needed to index. Search for complex queries is very
   difficult to execute.

For most deployments, *sharding by document is the preferred approach*
for providing distributed indexing.

In addition to distributed indexing, search queries must be spread and
routed to the relevant search nodes. The options for **distributed
search** are:

1. Dedicated load-balancer(s) in front of the search nodes. The corpus
   is broken into N shards, each replicated R times, for a total of
   RxN search nodes. A load-balancer picks one of the shard replica
   sets, and then fans out the query to the N shards in the replica
   set. This design introduces an additional point of complexity and
   is complex to scale elastically, but provides the best-possible
   query latency. This is the approach that Solr and Solandra follow.

                                       query
                                         |
                                         |
                                         v
                             replica balancing server
                             |                     |
                             |                     |
                             v                     v
          shard routing web-server                shard routing web server
           |         |         |                   |         |         |
           |         |         |                   |         |         |
           v         v         v                   v         v         v
          shard     shard     shard              shard     shard     shard

1. Every search node is a peer and capable of answering any query, and
   the search node's storage system provides the distribution
   mechanisms for the index. This is simple from a serving standpoint,
   allows elastic cluster operations, but introduces additional
   latency. This is the approach that ElasticSearch and LuceneHbase
   follow.

                                        query
                                          |
                                          |
                                          v
                     layer 3 direct server return load balancer
                     |           |            |             |
                     |           |            |             |
                     v           v            v             v
                    node        node         node         node
                     |           |            |             |
                     |           |            |             |
                     v           v            v             v
                    search index in elastic distributed storage

In [Apache Lucene](http://lucene.apache.org/), the index and search
design looks like this:

    {doc} --> IndexWriter --> FSDirectory <-- IndexReader <-- IndexSearcher <-- {query}
                                  |
                                  |
                                  v
                                disk

In a load-balanced architecture, we can split the search index across
Lucene instances and have the load balancer route and spread queries.
This is powerful and extremely scalable, but architecturally it makes
it more complex to scale elastically, as rebalancing shards is hard
since the index needs to be fully recomputed. Solr follows this
design.

When following a peer-based search node design, there are two possible
ways of performing distributed indexing with Lucene:

1. Implementing custom `IndexWriter` and `IndexReader`, i.e. there are
   no index segment files, distribution is solved by an underlying
   distributed store and the indices are stored in a format optimized
   for that distributed store. This is relatively simple and is what
   Solandra and HBasene do. See
   [[article on LuceneHbase](http://www.infoq.com/articles/LuceneHbase)]
   for details. In this design, all search nodes are equal as the
   IndexReader reroutes behind the scenes.

        {doc} --> IndexWriter --> FSDirectory <-- IndexReader <-- IndexSearcher <-- {query}
                      |                                |
                      |                                |
                      v                                v
                 Custom IndexWriter             Custom IndexReader
                      |                                |
                      |                                |
                      -----> Distributed Storage <------

1. Implementing custom `FSDirectory`, i.e. index segment files are
   distributed across filesystems on multiple nodes. This is simple
   architecturally but harder to implement than (1). This is what
   ElasticSearch does. In this design, all nodes are "equal" and can
   be used for querying, as `FSDirectory` hides the distributed store.

        {doc} --> IndexWriter --> FSDirectory <-- IndexReader <-- IndexSearcher <-- {query}
                                      |
                                      |
                                      v
                             Distributed storage

## Concerns ##

To be able to provide a distributed search system, these are the usual
concerns we should look at:

* Distributed indexing
* Distributed querying
* Near real-time indexing
* Faceted search
* Hadoop and HBase friendly
* Custom scoring algorithms
* Custom indexing algorithms
* Maintainability
* Operability

## Alternatives ##

In the open source space, these are the current leading alternatives (full search systems):

* Solr
* ElasticSearch
* Solandra
* HBasene
* Sensei (Zoie, Bobo)
* IndexTank
* Lily

### Solr ###

[Solr](http://lucene.apache.org/solr/) is the grandfather of all the
Lucene-based search systems. Now part of Apache, and originally
developed at CNET, Solr offers an HTTP indexer and query engine
running on top of Lucene and Jetty. Solr offers a lot of features and
has an active community. Historically Solr suffered from: (1) lack of
distributed indexing, (2) complex distributed search, and (3)
lock-collision between the indexer (writer) and the query engine
(reader).

Work has been done in trunk to introduce distributed search via
Zookeeper. Index segment files are stored in each solr host in the
file system, and Zookeper is used to coordinate the configuration.
Search nodes are aware of each other and a search query can be sent to
any node which will in turn distribute to all other nodes. To achieve
scalability and HA replicas can be created and Solr will automatically
load-balance.

As of late 2011, distributed indexing was still not available. See
[JIRA-2358](https://issues.apache.org/jira/browse/SOLR-2358). As a
result the client initiating the doc indexing is responsible for
distributing the indexing requests across the shards.

In regards to the index reader/writer collision, inserts and updates
may severely degrade read performance in Solr. By design, Solr is
optimized for fast search (reads), and therefore indexes new documents
as a batch, and installs a new version of the entire index. Installing
a new index is costly and no way near real-time. By design, Solr is
not trying to address this in the "persistent" form of the index (from
Solr's wiki):

>If you desire frequent new collections in order for your most recent
>changes to appear "live online", you must have both frequent
>commits/snapshots and frequent snappulls. The most frequently you can
>distribute index changes and maintain good performance is probably in
>the range of 1 to 5 minutes, depending on your reliance on caching
>for good query times, and the time it takes to autowarm those caches.

> Cache autowarming may be crucial to performance. On one hand a new
> cache version must be populated with enough entries so that
> subsequent queries will be served from the cache after the system
> switches to the new version of the collection. On the other hand,
> autowarming (populating) a new collection could take a lot of time,
> especially since it uses only one thread and one CPU. If your
> settings fire off snapinstaller too frequently, then a Solr slave
> could be in the undesirable condition of handing-off queries to one
> (old) collection, and, while warming a new collection, a second
> “new” one could be snapped and begin warming!

As of late 2011, in trunk we can find some near real-time features.
Soft commits are used to get the document in a near realtime view of
the index. Hard commits ensure that documents are on stable storage.
From the wiki:

> A common configuration might be to 'hard' auto commit every 1-10
> minutes and 'soft' auto commit every second. With this
> configuration, new documents will show up within about a second of
> being added, and if the power goes out, you will be certain to have
> a consistent index up to the last 'hard' commit.

In summary, pros:

* Large community support.
* Large deployments.
* Actively developed.
* Feature rich.
* Fast (caches index in-memory from disk).
* Zk-based distributed search.

Cons:

* No distributed indexing.
* Manual replication and sharding.
* Difficult to distribute NRT "soft" commit.
* Tuning for writes is very difficult.

### ElasticSearch ###

[ElasticSearch](http://www.elasticsearch.org/) offers an
out-of-the-box clustered search solution. Also, in contrast with Solr,
ES is optimized for near real-time search, i.e. updates (writes). ES
core is based on Netty and offers an HTTP JSON protocol and a native
thrift-based protocol. It uses an older version of Lucene that Solr,
which means some Solr features are not available.

ES fully leverages the `IndexWriter` and `IndexReader` from Lucene,
and provides a custom implementation of `FSDirectory` that ensure
replication and sharding.

ES nodes are discovered either via multicast at startup (a no-go for a
cloud network topology), or via configuration (not Zk). ES is designed
for all replica nodes to do the indexing to ensure a near real-time
index. Documents are indexed on a primary shard and propagated to all
replicas to ensure availability (index copies). ES manages failures
and keeps automatically rebalancing index segments in the cluster, by
splitting large indexes into smaller ones. Indices move as nodes are
added or removed. To be able to recover in case of failures, ES keeps
a long-term persistent copy of the indices in a "gateway" component.

ES is primarily developed by Shay Banon. The code is well documented,
and has good testing coverage. The user documentation is sufficient
but could be improved.

**Pros**:

* Distributed indexing.
* Distributed search.
* Near real-time.
* Active community.
* Large (?) deployments at StumbleUpon and Mozilla.
* Fast for big indices.
* Multi-tenancy.
* Operability.

**Cons**:

* Multicast-based or config-based node discovery.
* Documentation.
* Recovery from failure (from "gateway").

### Solandra ###

[Solandra](http://www.datastax.com/wp-content/uploads/2011/07/Scaling_Solr_with_Cassandra-CassandraSF2011.pdf)
is Solr on Cassandra. Solandra implements a custom `IndexReader` and
the `IndexWriter` that store the index in Cassandra (instead of using
segment files). Cassandra adds automatic sharding and replication, as
well as near real-time (as there is no commit). Solr runs _in_
Cassandra (same JVM).

**Pros**:

* Distributed indexing
* Distributed search
* Near real-time search

**Cons**:

* Slow
* Memory greedy
* Small community
* Support (?)
* Requires additional load-balancer
* Term-based partitioning
* By-passes most of Lucene's NRT index segment optimizations.

### HBasene ###

[HBasene](https://github.com/akkumar/hbasene) is architecturally
similar to Solandra, but using Hbase instead of Cassandra. HBasene
does not seem to be maintained.

### Sensei ###

[Sensei](http://senseidb.com/) is a search system from LinkedIn. It
uses Zoie for near real-time search indexing and Bobo for faceted
search. It follows the same approach as Solandra and HBasese, by
providing implementations of `IndexReader` and `IndexWriter` that
distribute the index. There is a small growing community. **There are
no unit tests in the open source version**.

### IndexTank ###

[IndexTank](https://github.com/linkedin/indextank-engine) wrote a
search engine from the ground up. IndexTank uses parts of Lucene: the
tokenizers, to be compatible with the query syntax, and the index
format for persistence on disk. **There are no unit tests in the open
source version**.

### Lily ###

[Lily](http://docs.outerthought.org/lily-docs-current/ext/toc/) is a
Solr based system. The index is stored in Solr, and the original
document in HBase. Lily adds automatic distributed indexing and
routing on top of Solr. It shares the same limitation with Solr that
it's not elastic:

> Shards cannot be added or removed on the fly: if you decide you want
> more or less shards, you need to define a new index and re-index
> your content into that new index. Nonetheless, Lily allows changing
> the sharding configuration of existing indexes on the fly without
> complaining. When doing this, working indexers will be restarted to
> take the new configuration into account (a running index re-building
> job would be unaffected). You have to consider yourself if the
> changes you make have sense without rebuilding the index.

## Summary ##

First in terms of high-level design choices:

* Document-based partitioning is the way to go for most use cases.
* Elasticity and multi-tenancy can only be achieved realistically in
  peer search node solutions.

In terms of implementation alternatives:

* I would rule out IndexTank and Sensei because of the no-availability
  of unit tests.
* I would rule out Solr and Lily because they do not offer a peer
  search solution.
* I would rule out Solandra because it requires Cassandra.

I feel that as of end of 2011, ElasticSearch and Lucene on HBase are
the best solutions to scaling search using open source solutions:

* ElasticSeach requires some work to add a more cloud-friendly node
  discovery mechanism and an ability to access the search index
  segments from Hadoop.
* Lucene on Hbase requires substantial work and ongoing support in
  order to be able to compete in performance and scalability (cost of
  scaling) with ElasticSearch, as less of Lucene's optimized index
  segment infrastructure is used.

## Other Resources ##

* [Lucene at twitter(PDF)](http://www.lucenerevolution.org/sites/default/files/Lucene%20Rev%20Preso%20Busch%20Realtime_Search_LR1010.pdf)
* [ElasticSearch and Solr feature comparison (Google Docs)](https://docs.google.com/present/view?id=dc6zhtt5_1frfxwfff&pli=1)
* [Google's search system design evolution (video)](http://videolectures.net/wsdm09_dean_cblirs/)
