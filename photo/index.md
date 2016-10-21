---
layout: archive
title: "Photo"
date: 2016-10-19T11:39:03-04:00
modified:
excerpt: "A collection of thoughts, inspiration, mistakes, and other minutia."
tags: []
image:
  feature:
  teaser:
---

<div class="tiles">
{% if site.categories.photo %}
  {% for post in site.categories.photo %}
    {% include post-grid.html %}
  {% endfor %}
{% else %}
    暂无图片
{% endif %}
</div><!-- /.tiles -->