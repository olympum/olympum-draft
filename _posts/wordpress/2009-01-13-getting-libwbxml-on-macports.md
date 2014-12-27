---
layout: post
title: Getting libwbxml on MacPorts
date: 2009-01-13 20:15:52.000000000 +00:00
categories:
- IMPS
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  _wp_old_slug: getting-libwxml-on-macports
  tmac_last_id: '531409168054231041'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415237302;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:129;}i:1;a:1:{s:2:"id";i:313;}i:2;a:1:{s:2:"id";i:116;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I need to be able to receive <code>wbxml</code> (binary XML) and transform it to xml using the IMPS 1.1/1.2/1.3 dictionary in Python. In PHP, I was using the PHP PECL extension <code>wbxml</code>, which uses <code>libwbxml</code> (<code>wbxml2</code>). In python, I need <code>pywbxml</code>. I like MacPorts, and I’ll use that instead of compiling myself the packages.

<ol>
<li><a href="http://www.macports.org/install.php">Install MacPorts</a>.</li>
<li>Self-update:
<pre><code>sudo port -v selfupdate
</code></pre>
</li>
<li>Some general goodness I can’t live without (wget will pull a long dependency list of things we’ll need for web development):
<pre><code>sudo port install wget
</code></pre>
</li>
<li>Wait.</li>
<li>Install wbxml
<pre><code>sudo port install wbxml2
</code></pre>
</li>
<li>And we get an error:
<pre><code>$ sudo port -v install wbxml2
---&gt;  Configuring wbxml2
Error: Target org.macports.configure returned: invalid command name "cd"
Warning: the following items did not execute (for wbxml2):
org.macports.activate org.macports.configure org.macports.build
org.macports.destroot org.macports.install
Error: Status 1 encountered during processing.
</code></pre>
</li>
</ol>
<p>So I filed a <a href="https://trac.macports.org/ticket/17984">ticket</a>. It seems like wbxml2 ownership moved to the <a href="http://libwbxml.opensync.org/">opensync folks</a> since the port was added. The port builds on 0.9.0 and the latest version is 0.10.1. I don’t much (nothing?) about MacPorts, but I went ahead and I patched it. You can find the patch on the <a href="https://trac.macports.org/ticket/17984">ticket</a> itself.</p>
<p>Finally, moving onto <code>pywbxml</code>. It seems the only maintained <code>pywbxml</code> code is from the <a href="http://www.synce.org/">synce</a> folks.</p>
<ol>
<li><a href="http://downloads.sourceforge.net/synce/pywbxml-0.1.tar.gz">Download pywbxml from sourceforge</a>.</li>
<li>Enter the <a href="http://www.olympum.com/imps/twisted-virtual-environment-goodness/">virtualenv</a>:
<pre><code>$ source ~/Sites/python/imps/bin/activate
</code></pre>
</li>
<li><code>pywbxml</code> needs pyrex, so we’ll install that first with:
<pre><code>$ easy_install pyrex
</code></pre>
</li>
<li>Install <code>pywbxml</code>:
<pre><code>$ tar xzfv pywbxml-0.1.tar.gz
$ cd pywbxml-0.1
$ ./configure
$ make
$ make install
</code></pre>
</li>
<li>Optionally, move the libraries to the virtualenv to keep things clean:
<pre><code>$ mv /Library/Python/2.5/site-packages/pywbxml.* \
    /Users/brunofr/Sites/python/imps/lib/python2.5/site-packages
</code></pre>
</li>
</ol>
<p>Now, we can test it:</p>
<pre id="scroll_to_here"><code>  $ python
  Python 2.5.1 (r251:54863, Apr 15 2008, 22:57:26)
  [GCC 4.0.1 (Apple Inc. build 5465)] on darwin
  Type "help", "copyright", "credits" or "license" for more information.
  &gt;&gt;&gt; from pywbxml import xml2wbxml, wbxml2xml
  &gt;&gt;&gt; xml = """&lt;?xml version="1.0"?&gt;&lt;!DOCTYPE WV-CSP-Message PUBLIC "-//OMA//DTD WV-CSP 1.2//EN" "http://www.openmobilealliance.org/DTD/WV-CSP.DTD"&gt;&lt;WV-CSP-Message xmlns="http://www.wireless-village.org/CSP1.1"&gt;&lt;Session&gt;&lt;SessionDescriptor&gt;&lt;SessionType&gt;Outband&lt;/SessionType&gt;&lt;/SessionDescriptor&gt;&lt;Transaction&gt;&lt;TransactionDescriptor&gt;&lt;TransactionMode&gt;Request&lt;/TransactionMode&gt;&lt;TransactionID&gt;nok1&lt;/TransactionID&gt;&lt;/TransactionDescriptor&gt;&lt;TransactionContent xmlns="http://www.wireless-village.org/TRC1.1"&gt;&lt;Login-Request&gt;&lt;UserID&gt;hermes.onesoup&lt;/UserID&gt;&lt;ClientID&gt;&lt;URL&gt;WV:IMPEC01$00001@NOK.S60&lt;/URL&gt;&lt;/ClientID&gt;&lt;Password&gt;xxxxxx&lt;/Password&gt;&lt;TimeToLive&gt;86400&lt;/TimeToLive&gt;&lt;SessionCookie&gt;wv:nokia.1789505498&lt;/SessionCookie&gt;&lt;/Login-Request&gt;&lt;/TransactionContent&gt;&lt;/Transaction&gt;&lt;/Session&gt;&lt;/WV-CSP-Message&gt;"""
  &gt;&gt;&gt; binary = xml2wbxml(xml)
  &gt;&gt;&gt; text = wbxml2xml(binary)
  &gt;&gt;&gt; binary
  '\x03\x01j\x00Imnp\x80\x19\x01\x01rtv\x80 \x01u\x03nok1\x00\x01\x01s\x00\x01]\x00\x00z\x03hermes.onesoup\x00\x01Jw\x03WV:\x00\x80\x12\x03PEC01$00001@NOK.S60\x00\x01\x01\x00\x01a\x03xxxxxx\x00\x01r\xc3\x03\x01Q\x80\x01p\x03wv:nokia.1789505498\x00\x01\x01\x01\x01\x01\x01'
  &gt;&gt;&gt; text
  '&lt;?xml version="1.0"?&gt;&lt;!DOCTYPE AirSync PUBLIC "-//AIRSYNC//DTD AirSync//EN" "http://www.microsoft.com/"&gt;&lt;Delete xmlns="http://synce.org/formats/airsync_wm5/airsync"&gt;&lt;unknown&gt;&lt;unknown&gt;&lt;unknown&gt;&lt;Truncation/&gt;&lt;/unknown&gt;&lt;/unknown&gt;&lt;unknown&gt;&lt;unknown&gt;&lt;unknown&gt;&lt;Supported/&gt;&lt;/unknown&gt;&lt;unknown&gt;nok1&lt;/unknown&gt;&lt;/unknown&gt;&lt;unknown&gt;&lt;Email3Address&gt;&lt;unknown&gt;hermes.onesoup&lt;/unknown&gt;&lt;Fetch xmlns="http://synce.org/formats/airsync_wm5/airsync"&gt;&lt;unknown&gt;WV:&lt;CollectionId/&gt;PEC01$00001@NOK.S60&lt;/unknown&gt;&lt;/Fetch&gt;&lt;HomeCity&gt;xxxxxx&lt;/HomeCity&gt;&lt;PagerNumber&gt;\x01Q\x80&lt;/PagerNumber&gt;&lt;OtherState&gt;wv:nokia.1789505498&lt;/OtherState&gt;&lt;/Email3Address&gt;&lt;/unknown&gt;&lt;/unknown&gt;&lt;/unknown&gt;&lt;/Delete&gt;'
</code></pre>
<p>It seems like it’s not using the WV CSP 1.1/1.2 dictionary (not surprising since I did not specify it anywhere). Looking at the code, in <code>pywbxml.pyx</code>, I can see:</p>
<pre><code>  params.lang = WBXML_LANG_AIRSYNC
</code></pre>
<p>So, whereas the PHP PECL <code>wbxml</code> extension is exposing all the parameters in <code>libwbxml</code>, it seems like the Python version <code>pywbxml</code> is not, and it’s hard-coding assumptions.</p>
<p>Lesson learned with my day on python, twisted, wbxml, etc.: spending my time fixing the basics, does not allow me to work on the problems I need to solve. Will I fix <code>pywbxml</code>? I don’t know, but most likely not.</p>
