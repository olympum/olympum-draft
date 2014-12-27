---
layout: post
title: Quick benchmark checkpoint on Java and NodeJS
date: 2011-01-23 19:46:58.000000000 +00:00
categories:
- Java
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409146977865728'
  _wpcom_is_markdown: '1'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415225869;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:328;}i:1;a:1:{s:2:"id";i:315;}i:2;a:1:{s:2:"id";i:313;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

First, in Java (my nodejs-inspired NIO/Netty based HTTP server):

{% highlight java %}
Server server = Http.createServer();
server.setRequestListener(new RequestListener() {
    @Override
    public void service(ServerRequest request, ServerResponse response) {
        HashMap<String, String> headers = new HashMap<String, String>();
        headers.put("Content-Type", "text/html; charset=utf-8");
        headers.put("Content-Length", "47");
        response.writeHeader(200, headers);
        response.end("<html><body><h1>hello world</h1></body></html>");
    }
});
server.listen(8080);
{% endhighlight %}

Now, in Javascript:

{% highlight js %}
http.createServer(function(req, res) {
    res.writeHead(200, {"Content-Length": "47",
                        "Content-Type": "text/html; charset=utf-8"});
    res.write("<html><body><h1>hello world</h1></body></html>");
    res.end();
}).listen(8080);
{% endhighlight %}

A quick "smoke" benchmark results using ab (MBA, 2 cores, 10.6.6, 4 GB, 2.13 GHz). First Java:

{% highlight bash %}
$ ab -k -n 2000 -c 200  http://localhost:8080/
Time taken for tests:   0.127 seconds
Complete requests:      2000
Failed requests:        0
Write errors:           0
Keep-Alive requests:    2000
Total transferred:      305850 bytes
HTML transferred:       95833 bytes
Requests per second:    15693.29 [#/sec] (mean)
Time per request:       12.744 [ms] (mean)
Time per request:       0.064 [ms] (mean, across all concurrent requests)
Transfer rate:          2343.65 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   1.6      0      10
Processing:     1    5   2.9      5      16
Waiting:        1    5   2.9      5      16
Total:          1    6   3.4      5      19
{% endhighlight %}

and then nodejs (kriszyp/multi-node using node 0.2.5 on 2 nodes):

{% highlight bash %}
$ ab -k -n 2000 -c 200 http://127.0.0.1:8080/
Time taken for tests:   0.225 seconds
Complete requests:      2000
Failed requests:        0
Write errors:           0
Keep-Alive requests:    2000
Total transferred:      300150 bytes
HTML transferred:       94047 bytes
Requests per second:    8876.38 [#/sec] (mean)
Time per request:       22.532 [ms] (mean)
Time per request:       0.113 [ms] (mean, across all concurrent requests)
Transfer rate:          1300.90 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    1   1.9      0      11
Processing:     0   18   3.7     18      28
Waiting:        0   18   3.7     18      28
Total:          0   18   4.5     18      39
{% endhighlight %}

So far, so good. I can now start adding Rhino.
