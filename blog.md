---
layout: page
title: Blog
permalink: blog
---
<div class="max-w-2xl mx-auto space-y-6">
  {% for post in site.posts %}
    <a 
      href="{{ site.baseurl }}{{ post.url }}"
      class="block border-b pb-4 hover:bg-gray-50 transition rounded"
    >
      <h3 class="text-xl font-bold text-gray-800">
        {{ post.title }}
      </h3>
      <div class="text-xs text-gray-400 mt-2">
        {{ post.date | date: "%B %-d, %Y" }}
      </div>
    </a>
  {% endfor %}
</div>
