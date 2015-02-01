---
layout: page
title: 快速方便记录点点滴滴!
---
{% include JB/setup %}
## 未分类列表

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## Useful links

[Jekyll Quick Start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)

[Jekyll Bootstrap](http://jekyllbootstrap.com)

[jekyll-bootstrap themes](http://github.com/plusjade/jekyll-bootstrap)
