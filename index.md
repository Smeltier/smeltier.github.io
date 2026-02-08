---
layout: default
title: Home
---

# Olá, eu sou o Gabriel Gonçalves

Sou estudante de Engenharia de Computação no CEFET-MG, curto algoritmos e estruturas de dados.

## POSTS:

{% for post in site.posts %}

- [{{ post.title }}]({{ post.url }})
  <small>{{ post.date | date: %d/%m/%Y }}</small>
  {% endfor %}
