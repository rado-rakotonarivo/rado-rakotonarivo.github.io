---
layout: default
title: Blog
permalink: /blog
---

[<< Get back to Teaching](/teaching)

<h2 class="listing"> Billets pour les étudiants </h2>

<br/>

<ul>
  {% for post in site.posts %}
  <li style="list-style-type: circle"><a href="{{ post.url }}" class="post-preview">{{ post.title }}</a> [{{ post.date }}]</li>
  {% endfor %}
</ul>
