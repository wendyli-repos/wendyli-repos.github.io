---
layout: page
title: Articles
permalink: /article/
---

<ul>
  {% for post in site.posts %}
    <li>
      <h4><span >{{ post.date | date: "%Y-%m-%d"}}</span> <a href="{{ post.url }}">{{ post.title }}</a></h4>
    </li>
  {% endfor %}
</ul>
