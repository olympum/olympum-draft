---
layout: page
title: "Topics"
description: "Topics I Cover"
header-img: "img/topics.jpg"
---

{% for category in site.categories %}
<div class="post-preview">
	<a name="{{ category | first }}">
        <h2 class="post-title">
			{{ category | first | capitalize }}
        </h2>
	</a>
	{% for posts in category %}
	<ul>
      {% for post in posts %}
	  	{% if post.url %}
			<li class="post-meta"><a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date: "%B %-d, %Y" }})</li>
		{% endif %}
      {% endfor %}
	</ul>
    {% endfor %}
</div>
	  
{% endfor %}
