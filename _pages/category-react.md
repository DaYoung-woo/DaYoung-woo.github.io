---
layout: category
title: "react"
category: react
permalink: /category/react/
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