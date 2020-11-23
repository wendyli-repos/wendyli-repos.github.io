---
layout: page
title: Categories
permalink: /categories/
---

{% assign categories_list = site.categories %}
{% for category in categories_list %}
  <ul style="font-weight:bold; display: inline-block; background-color: lightgrey" >{{ category[0] | upcase }} 
    <li style="list-style-type: none; display: inline-block" class="post_count">{{ category[1].size }}</li>
  </ul>
{%- endfor -%}

{%- for category in categories_list -%}

  <h3>{{ category[0] | upcase }} <span class="post_count">{{ category[1].size }}</span></h3>
  <ul>
    {% for post in category[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {%- endfor -%}
  </ul>
{%- endfor -%}


