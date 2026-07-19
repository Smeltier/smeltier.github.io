---
layout: default
title: Home
---

Bem-vindo

Este site é meu caderno público.

Uso para registrar estudos, experimentar ideias e documentar projetos.
Se algo aqui te ajudar, ótimo.
Se algo estiver errado, provavelmente ainda estou aprendendo.

Abaixo estão os **posts**, organizados do mais recente para o mais antigo.
Se quiser saber mais sobre mim, a página **About** funciona como um pseudo-currículo.
Já a aba **Projects** reúne os projetos que uso como prática e portfólio.

## POSTS

<ul>
  {% assign total = site.posts | size %}
  {% for post in site.posts %}
    <li>
      {{ total | minus: forloop.index0 }}. <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
