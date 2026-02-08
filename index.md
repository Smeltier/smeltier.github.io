---
layout: default
title: Home
---

[Sobre mim](/about)
[Projetos](/projects)

## POSTS:

{% for post in site.posts %}

- [{{ post.title }}]({{ post.url }})
  <small>{{ post.date | date: %d/%m/%Y }}</small>
  {% endfor %}
