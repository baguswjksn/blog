---
layout: page
title: Blog
permalink: blog
---

<div>
  {% for post in site.posts %}
    <div class="py-2">
      <h3 class="text-gray-800 hover:text-gray-600">
        <a href="{{site.baseurl}}{{ post.url }}">{{ post.title}}</a>
      </h3>
      <div class="text-sm text-gray-500">{{post.date | date: "%B %-d, %Y"}}</div>
    </div>
  {% endfor %}
</div>
