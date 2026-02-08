---
layout: default
title: Projetos
permalink: /projects/
---

# Projetos

{% for projects in site.projects %}

## [{{ projects.title }}]({{ projects.url }})

{{ project.description }}

[GitHub]({{ project.github }})

---

{% endfor %}
