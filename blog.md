---
layout: page
title: Blog
permalink: blog
---
<div class="max-w-2xl mx-auto space-y-6">
  {% for post in site.posts %}
      <a href="{{ site.baseurl }}{{ post.url }} class="text-xl font-bold text-gray-800">
        {{ post.title }}
      </a>
      <div class="text-xs text-gray-400 mt-2">
        {{ post.date | date: "%B %-d, %Y" }}
      </div>
  {% endfor %}
</div>
