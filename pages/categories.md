---
layout: categories
title: Categories
description: 哈哈，你找到了我的文章基因库
keywords: 分类
comments: false
menu: 分类
permalink: /categories/
---

<section class="container posts-content">
{% assign sorted_categories = site.categories | sort %}
{% for category in sorted_categories %}
<h3>{{ category | first }}</h3>
<ol class="posts-list" id="{{ category[0] }}">
{% for jottings in category.last %}
<li class="posts-list-item">
<span class="posts-list-meta">{{ jottings.date | date:"%Y-%m-%d" }}</span>
<a class="posts-list-name" href="{{ site.url }}{{ jottings.url }}">{{ jottings.title }}</a>
</li>
{% endfor %}
</ol>
{% endfor %}
</section>
<!-- /section.content4 -->
<section class="container posts-content">
{% assign sorted_jottings = site.jottings | sort %}
{% for jottings in sorted_jottings %}
{% if jottings.categories == "随笔" %}
<h3>{{jottings.categories}}</h3>
<ol class="posts-list" id="{{ jottings.categories }}">
<li class="posts-list-item">
<span class="posts-list-meta">{{ jottings.date | date:"%Y-%m-%d" }}</span>
<a class="posts-list-name" href="{{ site.url }}{{ jottings.url }}">{{ jottings.title }}</a>
</li>
</ol>
{% endif %}
{% if jottings.categories == "诗集" %}
<h3>{{jottings.categories}}</h3>
<ol class="posts-list" id="{{ jottings.categories }}">
<li class="posts-list-item">
<span class="posts-list-meta">{{ jottings.date | date:"%Y-%m-%d" }}</span>
<a class="posts-list-name" href="{{ site.url }}{{ jottings.url }}">{{ jottings.title }}</a>
</li>
</ol>
{% endif %}
{% endfor %}
</section>
<!-- /section.content5 -->