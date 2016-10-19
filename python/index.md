---
layout: archive
title: "Python"
date: 2016-10-19T11:39:03-04:00
modified:
excerpt: "A collection of thoughts, inspiration, mistakes, and other minutia."
tags: []
image:
  feature:
  teaser:
---

<div class="tiles">
{% if site.categories.python %}
  {% for post in site.categories.python %}
    {% include post-grid.html %}
  {% endfor %}
{% else %}
    暂无文章
{% endif %}
</div><!-- /.tiles -->