---
layout: default
title: Home
---

## POSTS:

<ul>
  {% assign total = site.posts | size %}
  {% for post in site.posts %}
    <li>
      {{ total | minus: forloop.index0 }}. <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
