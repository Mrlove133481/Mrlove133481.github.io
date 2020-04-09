---
layout: page
title: Jottings
description: 归来仍是少年
keywords: 随笔, Jottings
comments: false
menu: 随笔
permalink: /jottings/
---

> 记多少命令和快捷键会让脑袋爆炸呢？

<ul class="listing">
{% for jottings in site.jottings %}
{% if jottings.title != "Jottings Template" %}
<li class="listing-item"><a href="{{ site.url }}{{ jottings.url }}">{{ jottings.title }}</a></li>
{% endif %}
{% endfor %}
</ul>

