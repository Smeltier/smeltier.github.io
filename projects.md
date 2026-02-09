---
layout: default
title: Projetos
permalink: /projects/
---

# Projetos

{% for project in site.projects %}

## [{{ project.title }}]({{ project.url }})

{{ project.description }}

[GitHub]({{ project.github }})

---

{% endfor %}
