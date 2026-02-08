---
layout: default
title: Home
---

[Sobre mim](/about)

## POSTS:

{% for post in site.posts %}

- [{{ post.title }}]({{ post.url }})
  <small>{{ post.date | date: %d/%m/%Y }}</small>
  {% endfor %}
