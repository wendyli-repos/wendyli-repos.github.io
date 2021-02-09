---
layout: page
title: Archives
permalink: /archives/
---
<!-- List post by published date -->
<!-- 
<ul>
  {% for post in site.posts %}
    <li>
      <h4><span >{{ post.date | date: "%Y-%m-%d"}}</span> <a href="{{ post.url }}">{{ post.title }}</a></h4>
    </li>
  {% endfor %}
</ul> -->

<!-- Total: {{ site.posts | size }} <a href="{{ site.base_url }}/tags/">posts</a>:  -->

***

<!-- Listing posts by published year -->
{% for post in site.posts %}
  {% capture currentyear %}{{post.date | date: "%Y"}}{% endcapture %}
  {% if currentyear != year %}
     {{ currentyear }}
    {% capture year %}{{currentyear}}{% endcapture %} 
  {% endif %}
  <ul class="posts-in-year">
        <li>
      <h4><span >{{ post.date | date: "%Y-%m-%d"}}</span> <a href="{{ post.url }}">{{ post.title }}</a></h4>
    </li>
  </ul>
{% endfor %}