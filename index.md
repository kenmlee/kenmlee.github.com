---
layout: page
title: 快速方便记录点点滴滴!
---
{% include JB/setup %}
## 记录
{% for post in site.categories.blog %}
### {{ post.date | date_to_string }}: [{{ post.title }}]({{ BASE_PATH }}{{ post.url }}) 

> {{ post.excerpt | strip_html }}

{% endfor %}

## 兴趣
{% for post in site.categories.bookmark %}
### {{ post.date | date_to_string }}: [{{ post.title }}]({{ BASE_PATH }}{{ post.url }}) 

> {{ post.excerpt | strip_html }}

{% endfor %}

### Useful links

[Jekyll Quick Start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)

[Jekyll Bootstrap](http://jekyllbootstrap.com)

[jekyll-bootstrap themes](http://github.com/plusjade/jekyll-bootstrap)
