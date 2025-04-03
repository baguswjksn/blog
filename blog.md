---
layout: page
title: Blog
permalink: blog
---
<div class="max-w-2xl mx-auto space-y-6">
  {% for post in site.posts %}
    <div 
      class="border-b pb-4 hover:shadow-md transition-shadow duration-300 cursor-pointer"
      onclick="window.location.href='{{ site.baseurl }}{{ post.url }}'"
    >
      <h3 class="text-xl font-semibold text-gray-900 hover:text-gray-700 transition-colors duration-200">
        {{ post.title }}
      </h3>
      <p class="text-gray-600 text-sm mt-1">{{ post.desc }}</p>
      <div class="text-xs text-gray-400 mt-2">{{ post.date | date: "%B %-d, %Y" }}</div>
    </div>
  {% endfor %}
</div>
