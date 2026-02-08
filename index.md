---
layout: default
title: Home
---

## POSTS:

<ul>
  {% assign posts = site.posts | sort: "date" | reverse %}
  {% for posts in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
