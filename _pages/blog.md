---
layout: default
title: Blog
permalink: /blog
---

[<< Get back to Teaching](/teaching)

## Billets pour les étudiants

<ul>
  {% for post in site.posts %}
  <li><a href="{{ post.url }}" class="post-preview">{{ post.title }}</a></li>
  {% endfor %}
</ul>
