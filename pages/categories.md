---
layout: categories
title: 文章分类
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
{% for posts in category.last %}
<li class="posts-list-item">
<span class="posts-list-meta">{{ posts.date | date:"%Y-%m-%d" }}</span>
<a class="posts-list-name" href="{{ site.url }}{{ posts.url }}">{{ posts.title }}</a>
</li>
{% endfor %}
</ol>
{% endfor %}
</section>
<!-- /section.content4 -->
<section class="container posts-content">
<h3>短文</h3>
<ol class="posts-list" id="短文">
{% for jottings in site.jottings %}
{% if  jottings.categories[0] == "短文" %}
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
<!-- /section.content7 -->