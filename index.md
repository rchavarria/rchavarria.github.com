---
layout: default
---

{% for post in site.posts limit:25 %}
{% include article.html %}
{% endfor %}

<hr>

Ver [todos los posts por categoría]({{ site.baseurl | append:"/all" }}), o ver
[todos ordenados por fecha]({{ site.baseurl | append:"/archives" }}).
