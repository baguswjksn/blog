---
layout: page
title: Blog
permalink: blog
---

{% assign featured_posts = site.posts | where: "featured", true %}

<div class="mb-8">
    <!-- Tab navigation with major spacing -->
    <div style="border-bottom: 1px solid #e5e7eb;">
        <nav style="display: flex; justify-content: center; margin-bottom: -1px;">
            <div style="display: flex; gap: 6rem;">
                <a id="all-label" href="javascript:void(0)" onclick="showTab('all')"
                    style="border-bottom: 2px solid #4f46e5; padding: 1rem 0.25rem; font-size: 0.875rem; font-weight: 500; color: #4f46e5; white-space: nowrap; text-decoration: none;"
                    aria-current="page">All Posts</a>
                <a id="featured-label" href="javascript:void(0)" onclick="showTab('featured')"
                    style="border-bottom: 2px solid transparent; padding: 1rem 0.25rem; font-size: 0.875rem; font-weight: 500; color: #6b7280; white-space: nowrap; text-decoration: none;">Selected</a>
            </div>
        </nav>
    </div>


  <!-- Featured Tab Content -->
  <div id="featured-tab" class="tab-content">
      {% if featured_posts.size > 0 %}
      <!-- <div class="grid md:grid-cols-2 gap-6"> -->
        <div data-lang="id" class="hidden">
      {% for post in featured_posts %}
<div>
    <h3 style="display: flex; align-items: center; gap: 0.5rem; flex-wrap: wrap;">
        <a href="{{site.baseurl}}{{ post.url }}" style="color: black; text-decoration: none;">
            <strong>{{ post.id-title }}</strong>
        </a>
        <span class="text-xs text-gray-500">
            {{ post.date | date: "%B %-d, %Y" }}
        </span>
    </h3>
    <div class="text-sm text-gray-400">{{ post.id-desc }}</div>
</div>
      {% endfor %}
      </div>

<div data-lang="en">
      {% for post in featured_posts %}
<div>
    <h3 style="display: flex; align-items: center; gap: 0.5rem; flex-wrap: wrap;">
        <a href="{{site.baseurl}}{{ post.url }}" style="color: black; text-decoration: none;">
            <strong>{{ post.en-title }}</strong>
        </a>
        <span class="text-xs text-gray-500">
            {{ post.date | date: "%B %-d, %Y" }}
        </span>
    </h3>
    <div class="text-sm text-gray-400">{{ post.en-desc }}</div>
</div>

{% endfor %}
</div>
<!-- </div> -->
{% else %}
<p class="text-gray-500 italic">No featured posts yet.</p>
{% endif %}

  </div>


<div id="all-tab" class="tab-content hidden">
<div data-lang="id" class="hidden">
    {% for post in site.posts %}
<div>
    <h3 style="display: flex; align-items: center; gap: 0.5rem; flex-wrap: wrap;">
        <a href="{{site.baseurl}}{{ post.url }}" style="color: black; text-decoration: none;">
            <strong>{{ post.id-title }}</strong>
        </a>
        <span class="text-xs text-gray-500">
            {{ post.date | date: "%B %-d, %Y" }}
        </span>
    </h3>
    <div class="text-sm text-gray-400">{{ post.id-desc }}</div>
</div>
{% endfor %}
    </div>

<div data-lang="en">
    {% for post in site.posts %}
<div>
    <h3 style="display: flex; align-items: center; gap: 0.5rem; flex-wrap: wrap;">
        <a href="{{site.baseurl}}{{ post.url }}" style="color: black; text-decoration: none;">
            <strong>{{ post.en-title }}</strong>
        </a>
        <span class="text-xs text-gray-500">
            {{ post.date | date: "%B %-d, %Y" }}
        </span>
    </h3>
    <div class="text-sm text-gray-400">{{ post.en-desc }}</div>
</div>
    {% endfor %}
    </div>

</div>

<script>
    function showTab(tabName) {
        // Hide all tabs
        const tabContents = document.querySelectorAll('.tab-content');
        tabContents.forEach(tab => tab.classList.add('hidden'));

        // Show the selected tab
        const selectedTab = document.getElementById(tabName + '-tab');
        if (selectedTab) {
            selectedTab.classList.remove('hidden');
        }

        // Reset all tab styles
        document.getElementById('featured-label').style.borderBottomColor = 'transparent';
        document.getElementById('featured-label').style.color = '#6b7280';
        document.getElementById('all-label').style.borderBottomColor = 'transparent';
        document.getElementById('all-label').style.color = '#6b7280';

        // Activate the selected tab
        document.getElementById(tabName + '-label').style.borderBottomColor = '#4f46e5';
        document.getElementById(tabName + '-label').style.color = '#4f46e5';
    }

    // Initialize tabs - make All Posts the default
    document.addEventListener('DOMContentLoaded', function () {
        showTab('all');
    });
</script>

<style>
    .active {
        font-weight: 500;
        color: #4f46e5;
        border-bottom: 2px solid #4f46e5;
    }
</style>

{% include sticky-bottom.html %}