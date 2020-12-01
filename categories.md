---
layout: page
title: Categories
permalink: /categories/
---
Total {{ site.categories | size }} different <a href="{{ site.base_url }}/categories/">categories</a>:

***

{% assign categories_list = site.categories %}
{% for category in categories_list %}
  <ul style="display: inline-block; text-decoration: underline;" >{{ category[0] | upcase }} 
    <li style="list-style-type: none; display: inline-block;" class="post_count">{{ category[1].size }}</li>
  </ul>
{%- endfor -%}

{%- for category in categories_list -%}
  <h3>{{ category[0] | upcase }} <span class="post_count"> • ({{ category[1].size }})</span></h3>
  <ul>
    {% for post in category[1] %}
      <li style="list-style-type: none;"><a href="{{ post.url }}">{{ post.title }}</a></li>
    {%- endfor -%}
  </ul>
{%- endfor -%}


