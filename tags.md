---
layout: page
title: Tags
permalink: /tags/
---
Total {{ site.tags | size }} <a href="{{ site.base_url }}/tags/">tags</a>:

***

{% capture temptags %}
  {% for tag in site.tags %}
    {{ tag[1].size | plus: 1000 }}#{{ tag[0] }}#{{ tag[1].size }}
  {% endfor %}
{% endcapture %}
{% assign sortedtemptags = temptags | split:' ' | sort | reverse %}
{% for temptag in sortedtemptags %}
  {% assign tagitems = temptag | split: '#' %}
  {% capture tagname %}{{ tagitems[1] }}{% endcapture %}
  <a href="/tag/{{ tagname }}" class="site-tag">{{ tagname }}</a>
{% endfor %}





