---
layout: default
title: Home
---

## POSTS:

<ul>
  {% for posts in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
