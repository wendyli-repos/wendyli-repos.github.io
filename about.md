---
layout: page
title: About
# permalink: /about/
---

# Hi,

welcome to my blog!

where I keep a record of my journey of learning IT stuff and notes<span>&#128394;</span>; also some brillant ideas<span>&#128161;</span> and awasome projects<span >&#x1F5A5;</span> .

# About me:

I am a career switcher from Construction to IT industry. The most fascnitating thing I like about Web Development is that no need to download or install anything before I can present greate things.

# Skills:

I am using
{% assign categories_list = site.categories %}
{%- for category in categories_list -%}
<span style="font-weight:bold; display: inline-block; background-color: lightgrey">{{ category[0] }} </span>
{% endfor %}
.

# About this blog:

I have posted total {{ site.posts | size }} <a href="{{ site.base_url }}/article/">posts</a> in {{ site.categories | size }} different <a href="{{ site.base_url }}/categories/">categories</a>. You can see all sorce code at [here](https://github.com/wendyli-repos/wendyli-repos.github.io).
