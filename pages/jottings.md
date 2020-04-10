---
layout: page
title: Jottings
description: 归来仍是少年
keywords: 随笔, Jottings
comments: false
menu: 随笔
permalink: /jottings/
---

> "寻了半生的春天,你一笑  便是了."

<ol class="posts-list" >
{% for jottings in site.jottings %}
{% if jottings.title != "Jottings Template" %}
<li class="listing-item">
<a  class="posts-list-name"  href="{{ site.url }}{{ jottings.url }}">{{ jottings.title }}</a>
<span class="posts-list-meta">&ensp;&ensp;{{ jottings.categories[0] }}</span>
<span class="posts-list-meta">{{ jottings.date | date:"%Y-%m-%d" }}</span>
</li>
{% endif %}
{% endfor %}
</ol>

