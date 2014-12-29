---
layout: page
title: "Essays"
description: "Short Writings and Musings"
header-img: "img/essays.jpg"
---

{% for post in site.essays %}
<div class="post-preview">
	<ul>
	  	{% if post.url %}
			<li class="post-meta"><a href="{{ post.url }}">{{ post.title }}</a> (last updated on {{ post.date | date: "%B %-d, %Y" }})</li>
		{% endif %}
	</ul>
</div>
{% endfor %}
