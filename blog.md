---
layout: page
title: Blog
permalink: blog
---

<div>
  {% for post in site.posts %}
    <div class="py-1">
<h3>
  <a href="{{site.baseurl}}{{ post.url }}" style="color: black; text-decoration: none;">
    <strong>{{ post.title }}</strong>
  </a>
</h3>
      <div class="text-sm text-gray-400">{{ post.desc }}</div>
    </div>
  {% endfor %}
</div>
