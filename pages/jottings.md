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

<section class="container posts-content">
<h3>随笔</h3>
<ol class="posts-list" id="随笔">
{% for jottings in site.jottings %}
{% if  jottings.categories[0] == "随笔" %}
<li class="posts-list-item">
<span class="posts-list-meta">{{ jottings.date | date:"%Y-%m-%d" }}</span>
<a class="posts-list-name" href="{{ site.url }}{{ jottings.url }}">{{ jottings.title }}</a>
</li>
{% endif %}
{% endfor %}
</ol>
<h3>诗集</h3>
<ol class="posts-list" id="诗集">
{% for jottings in site.jottings %}
{% if  jottings.categories[0] == "诗集" %}
<li class="posts-list-item">
<span class="posts-list-meta">{{ jottings.date | date:"%Y-%m-%d" }}</span>
<a class="posts-list-name" href="{{ site.url }}{{ jottings.url }}">{{ jottings.title }}</a>
</li>
{% endif %}
{% endfor %}
</ol>
</section>

