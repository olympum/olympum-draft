---
layout: post
title: Twisted Web IMPS Echo Client
date: 2009-01-13 14:36:54.000000000 +00:00
categories:
- Other
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409168054231041'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

Having a twisted environment, I have been able to write a simple web resource handler. I like twisted, although the documentation is pretty weak, so you have to go down to read the code rather frequently if you want to know how to do things.

<p>My first task was to handle an XML post for IMPS CSP. I thought I would skip the wbxml version to start with.</p>
<p>So first thing was to setup the test client. Just for now, I used <code>curl</code> to post the data:</p>
<pre><code>curl http://localhost:8080/ -d @login-success.in.txt
</code></pre>
<p>Where <code>login-success.in.txt</code> is the first message the phone sends in:</p>
<pre><code>&lt;?xml version="1.0"?&gt;
&lt;!DOCTYPE WV-CSP-Message PUBLIC "-//OMA//DTD WV-CSP 1.2//EN" "http://www.openmobilealliance.org/DTD/WV-CSP.DTD"&gt;
&lt;WV-CSP-Message xmlns="http://www.wireless-village.org/CSP1.1"&gt;
  &lt;Session&gt;
    &lt;SessionDescriptor&gt;
      &lt;SessionType&gt;Outband&lt;/SessionType&gt;
    &lt;/SessionDescriptor&gt;
    &lt;Transaction&gt;
      &lt;TransactionDescriptor&gt;
        &lt;TransactionMode&gt;Request&lt;/TransactionMode&gt;
        &lt;TransactionID&gt;nok1&lt;/TransactionID&gt;
      &lt;/TransactionDescriptor&gt;
      &lt;TransactionContent xmlns="http://www.wireless-village.org/TRC1.1"&gt;
        &lt;Login-Request&gt;
          &lt;UserID&gt;hermes.onesoup&lt;/UserID&gt;
          &lt;ClientID&gt;
            &lt;URL&gt;WV:IMPEC01$00001@NOK.S60&lt;/URL&gt;
          &lt;/ClientID&gt;
          &lt;Password&gt;xxxxxxx&lt;/Password&gt;
          &lt;TimeToLive&gt;86400&lt;/TimeToLive&gt;
          &lt;SessionCookie&gt;wv:nokia.1789505498&lt;/SessionCookie&gt;
        &lt;/Login-Request&gt;
      &lt;/TransactionContent&gt;
    &lt;/Transaction&gt;
  &lt;/Session&gt;
&lt;/WV-CSP-Message&gt;
</code></pre>
<p>The payload is contained within the POST data, but there are not arguments on it (no a=x). So I needed to get the raw content. To achieve that, I created a <code>hello.py</code> file which would contain my <code>Hello</code> resource handler:</p>
<pre name="code" class="python">
from twisted.web.resource import Resource

class Hello(Resource):
    allowedMethods = ('POST',)

    def render_POST(self, request):
        request.content.seek(0, 0)
        data = request.content.read()
        return data
</pre>
<p id="scroll_to_here">As we can see, all this does is to send the payload in the HTTP POST request back to the client. To get this running on twisted, we write an <code>index.rpy</code> and save it in <code>/Users/brunofr/Sites</code> (adjust):</p>
<pre><code>from imps.csp import hello

# comment the next line in production
reload(hello)
resource = hello.Hello()
</code></pre>
<p>A couple of comments about this code:</p>
<ol>
<li>I put the code within the <code>imps.csp</code> module.</li>
<li>I call <code>reload</code> to allow me to edit the module during development.</li>
</ol>
<p>And bang, we run it:</p>
<pre><code>twisted -n web --path=/Users/brunofr/Sites
</code></pre>
<p>Point your browser to <code>http://localhost:8080/</code>. It does not work, since we are not accepting the ‘GET’ method. But if you use <code>curl</code>:</p>
<pre><code>curl http://localhost:8080/ -d @login-success.in.txt
</code></pre>
<p>it works, as it should.</p>
