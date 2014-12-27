---
layout: post
title: pywbxml revisited
date: 2009-01-14 22:48:44.000000000 +00:00
categories:
- IMPS
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  tmac_last_id: '531409168054231041'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415291089;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:141;}i:1;a:1:{s:2:"id";i:10;}i:2;a:1:{s:2:"id";i:72;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I know I said I was not likely to fix <code>pywbxml</code>, but the
alternative was even less appealing. I <em>know</em> I have to move
away from Java, so here it is how to get pywbxml working.

<ol>
<li>Continuing to use a mix of Java and PHP to leverage the PHP PECL <code>wbxml</code> extension creates an unnecessary complexity.</li>
<li>Moving the PHP code doing <code>wbxml2xml</code> and <code>xml2wbxml</code> transformations to Java is possible but I noticed lack of activity on <a href="http://sourceforge.net/projects/kxml/">KML at sourceforge</a> (the project that contains the wbxml library for Java). <a href="http://libwbxml.opensync.org/">libwbxml</a> in contrast is owned and maintained by the opensync folks, and it’s only the python bindings that needed some love.</li>
<li>The XMPP library I use in Java, <a href="http://www.igniterealtime.org/projects/smack/index.jsp">Smack</a> uses a model of one-thread-per-socket, which for server-side and maintaining hundreds or thousands of users will require me to have much more memory in the box that I would like to. I rather use an event-based / reactor architectural style.</li>
</ol>
<p>So I decided to patch the Python bindings for my needs (rather than fixing it properly by exposing the args through the API). The Python bindings seem to be generated out of SWIG, so editing <code>src/pywbxml.pyx</code> is enough to get the dictionary I wanted for IMPS (<code>WBXML_LANG_WV_CSP12</code>). The change is straight forward, simply:</p>
<pre><code>params.lang = WBXML_LANG_WV_CSP12
</code></pre>
<p>or the unified patch:</p>
<pre><code>--- pywbxml-0.1/src/pywbxml.pyx 2006-07-28 01:51:57.000000000 +0100
+++ pywbxml-0.1-wv/src/pywbxml.pyx  2009-01-14 21:55:40.000000000 +0000
@@ -14,7 +14,7 @@
     object PyString_FromStringAndSize(char *s, int len)
     int PyString_AsStringAndSize(object obj, char **buffer, int *length)

-class WBXMLParseError:
+class WBXMLParseError(Exception):
     def __init__(self, code):
         self.code = code
         self.description = &lt;char *&gt; wbxml_errors_string(code)
@@ -28,7 +28,7 @@
     cdef WBXMLGenXMLParams params

     params.gen_type = WBXML_GEN_XML_CANONICAL
-    params.lang = WBXML_LANG_AIRSYNC
+    params.lang = WBXML_LANG_WV_CSP12
     params.indent = 0
     params.keep_ignorable_ws = 1
</code></pre>
<p>You will notice an additional change in the patch for WBXMLParseError - this comes from the Debian package, and ensures the we are raising a proper exception.</p>
<p>With this applied, compiled, and installed, I ran the same test with an IMPS CSP document, this time successfully:</p>
<pre id="scroll_to_here"><code>$ python
Python 2.5.1 (r251:54863, Apr 15 2008, 22:57:26)
[GCC 4.0.1 (Apple Inc. build 5465)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
&gt;&gt;&gt; from pywbxml import xml2wbxml, wbxml2xml
&gt;&gt;&gt; xml = """&lt;?xml version="1.0"?&gt;&lt;!DOCTYPE WV-CSP-Message PUBLIC "-//OMA//DTD WV-CSP 1.2//EN" "http://www.openmobilealliance.org/DTD/WV-CSP.DTD"&gt;&lt;WV-CSP-Message xmlns="http://www.wireless-village.org/CSP1.1"&gt;&lt;Session&gt;&lt;SessionDescriptor&gt;&lt;SessionType&gt;Outband&lt;/SessionType&gt;&lt;/SessionDescriptor&gt;&lt;Transaction&gt;&lt;TransactionDescriptor&gt;&lt;TransactionMode&gt;Request&lt;/TransactionMode&gt;&lt;TransactionID&gt;nok1&lt;/TransactionID&gt;&lt;/TransactionDescriptor&gt;&lt;TransactionContent xmlns="http://www.wireless-village.org/TRC1.1"&gt;&lt;Login-Request&gt;&lt;UserID&gt;hermes.onesoup&lt;/UserID&gt;&lt;ClientID&gt;&lt;URL&gt;WV:IMPEC01$00001@NOK.S60&lt;/URL&gt;&lt;/ClientID&gt;&lt;Password&gt;xxxxxx&lt;/Password&gt;&lt;TimeToLive&gt;86400&lt;/TimeToLive&gt;&lt;SessionCookie&gt;wv:nokia.1789505498&lt;/SessionCookie&gt;&lt;/Login-Request&gt;&lt;/TransactionContent&gt;&lt;/Transaction&gt;&lt;/Session&gt;&lt;/WV-CSP-Message&gt;"""
&gt;&gt;&gt; binary = xml2wbxml(xml)
&gt;&gt;&gt; text = wbxml2xml(binary)
&gt;&gt;&gt; text
'&lt;?xml version="1.0"?&gt;&lt;!DOCTYPE WV-CSP-Message PUBLIC "-//OMA//DTD WV-CSP 1.2//EN" "http://www.openmobilealliance.org/DTD/WV-CSP.DTD"&gt;&lt;WV-CSP-Message&gt;&lt;Session&gt;&lt;SessionDescriptor&gt;&lt;SessionType&gt;Outband&lt;/SessionType&gt;&lt;/SessionDescriptor&gt;&lt;Transaction&gt;&lt;TransactionDescriptor&gt;&lt;TransactionMode&gt;Request&lt;/TransactionMode&gt;&lt;TransactionID&gt;nok1&lt;/TransactionID&gt;&lt;/TransactionDescriptor&gt;&lt;TransactionContent&gt;&lt;Login-Request&gt;&lt;UserID&gt;hermes.onesoup&lt;/UserID&gt;&lt;ClientID&gt;&lt;URL&gt;WV:IMPEC01$00001@NOK.S60&lt;/URL&gt;&lt;/ClientID&gt;&lt;Password&gt;xxxxxx&lt;/Password&gt;&lt;TimeToLive&gt;86400&lt;/TimeToLive&gt;&lt;SessionCookie&gt;wv:nokia.1789505498&lt;/SessionCookie&gt;&lt;/Login-Request&gt;&lt;/TransactionContent&gt;&lt;/Transaction&gt;&lt;/Session&gt;&lt;/WV-CSP-Message&gt;'
</code></pre>
<p>Yes, I am now <em>happier</em>.</p>
