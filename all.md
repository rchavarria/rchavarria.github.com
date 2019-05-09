---
layout: default
title: "Artículos por categoría"
---

{% for category in site.categories %}
## {{ category | first }}
  {% for posts in category offset:1 %}
    {% for post in posts %}
- [{{ post.title }}]({{ site.baseurl | append:post.url }})
    {% endfor %}
  {% endfor %}
{% endfor %}
