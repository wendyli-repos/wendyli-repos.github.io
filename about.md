---
layout: page
title: About
# permalink: /about/
---

Hi, welcome to my blog where I keep a record of my journey of learning IT stuff and notes<span>&#128394;</span>; also some brillant ideas<span>&#128161;</span> and awasome projects<span >&#x1F5A5;</span> .

I have posted total {{ site.posts | size }} <a href="{{ site.base_url }}/article/">posts</a> in {{ site.categories | size }} different <a href="{{ site.base_url }}/categories/">categories</a>. 

I am using 
{% assign categories_list = site.categories %}
{%- for category in categories_list -%}
   <span style="font-weight:bold; display: inline-block; background-color: lightgrey">{{ category[0] }} </span>
{% endfor %}
.