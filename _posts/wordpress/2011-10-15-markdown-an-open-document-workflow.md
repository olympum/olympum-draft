---
layout: post
title: Markdown, An Open Document Workflow
date: 2011-10-15 14:27:55.000000000 +01:00
categories:
- Future
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409136601534466'
  _edit_last: '1'
  _wpcom_is_markdown: '1'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

I want to use a standard and open document format, so that I know I will be able to open my documents in years to come. That's plain text.
I also want to revision control my text files, so I want to use source control system. Which will also allow  me to synchronize between computers between computers.
I also like to have one standard editor I know I find in any operating system, and that will always work with my documents.
I want to make sure that I am not locked-in into any particular cloud or tool or format or ...

I've been using [Markdown](http://daringfireball.net/projects/markdown/) since 2006, effectively taking all my notes at work
using a simple text editor and using the Markdown text markup format. I also
use Markdown for writing down thoughts and posting to this blog. I rarely,
if ever, use Word or even TeX/LaTeX. I treat markdown as my source format
and I generate all my target formats using <a href="http://fletcherpenney.net/multimarkdown/">multimarkdown</a>: PDF, HTML, RTF,
etc.

As an editor, I use <a href="http://jblevins.org/projects/markdown-mode/">emacs markdown
mode</a> and it does me well. And
it's not about <a href="http://www.gnu.org/s/emacs/">emacs</a>: you may use
<a href="http://www.vim.org/">vi</a>, or <a href="http://macromates.com/">TextMate</a>, or whatever.
The point is that your favorite text editor, whichever it is, is probably good
enough. I have also recently started using <a href="http://markedapp.com/">Marked</a> as
a convenience for previewing the transformed markdown output without having to
continuously switch back to the browser or do <code>C-c C-c p</code> all the time.

I also use <a href="http://jekyllrb.com/">Jekyll</a> to transform some of my markdown
text files onto a static site where <a href="http://git-scm.com/">git</a> is the glue
here. It works everywhere I have git.

Recently I have had a need to bring my markdown files to the iPhone and the
iPad. And although one may find some specialized git iOS clients for things
like <a href="https://github.com/">github</a>, there is no general git client for iOS,
integrated with a text viewer, as far as I know.

Given the lack of shared file system in iOS, whichever app I use must have
both text editor, ideally with support for markdown preview, as well as sync
capabilities. <a href="http://itunes.apple.com/us/app/id396073482?mt=8">Nocs</a> is
exactly that. It uses <a href="http://db.tt/4rTs9QST">Dropbox</a> to sync your files, and
it has an embedded text editor with markdowns support. It fits perfectly into
my workflow. I continue to use emacs on the laptop, and Nocs on the iPad.
Dropbox syncs between laptop and tablet, and git between computers.

I am sure there are ways I could simplify the flow. But for now, this meets my
requirements.

Finally, I am not keen at all to use tools like <a href="http://www.evernote.com/">Evernote</a>, since as far as I am concerned I am
losing both freedom and the future-proof aspects of plain text. I have
literally thousands of text notes accumulated over the years, and I have the
reassurance that I will always be able to access and edit my notes in years to
come. I don't want to risk putting my documents onto a proprietary platform.
