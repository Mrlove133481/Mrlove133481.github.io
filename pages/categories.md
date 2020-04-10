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
<ul class="listing">
{% for jottings in site.jottings %}
{% if jottings.title != "Jottings Template" %}
<li class="listing-item"><a href="{{ site.url }}{{ jottings.url }}">{{ jottings.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
</section>
<!-- /section.content6 -->