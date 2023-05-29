---
layout: category
title: "vue3"
category: vue3
permalink: /category/vue3/
---
<h1>{{ page.title }}</h1>

<ul>
  {% for post in site.posts %}
    {% if post.category == page.category %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endif %}
  {% endfor %}
</ul>
