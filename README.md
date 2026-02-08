---
layout: default
title: Home
---

# smeltier.github.io

{% for post in site.posts %}

- [{{ post.title }}]({{ post.url }})
  <small>{{ post.date | date: %d/%m/%Y }}</small>
  {% endfor %}

