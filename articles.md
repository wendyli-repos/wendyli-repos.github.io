---
layout: page
title: Articles
permalink: /article/
---

<ul>
  {% for post in site.posts %}
    <li>
      <h3><a href="{{ post.url }}">{{ post.title }}</a> <span style="font-size: small">{{ post.date | date: "%-d %b, %Y"}}</span></h3>
    </li>
  {% endfor %}
</ul>
