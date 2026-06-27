---
layout: default
permalink: /blog/
title: blog
nav: true
nav_order: 1
pagination:
  enabled: true
  collection: posts
  permalink: /page/:num/
  per_page: 5
  sort_field: date
  sort_reverse: true
  trail:
    before: 1 # The number of links before the current page
    after: 3 # The number of links after the current page
---

<div class="post">
  <header class="post-header">
    <h1 class="post-title">{{ site.blog_name }}</h1>
    {% if site.blog_description %}
      <p class="desc">{{ site.blog_description }}</p>
    {% endif %}
  </header>

  {% if page.pagination.enabled %}
    {% assign postlist = paginator.posts %}
  {% else %}
    {% assign postlist = site.posts %}
  {% endif %}

  <div class="project-list">
    {% for post in postlist %}
      {% assign preview_text = post.description | default: post.excerpt | strip_html | truncate: 160 %}
      <div class="project-item">
        <h3 class="project-title">
          {% if post.redirect == blank %}
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          {% elsif post.redirect contains '://' %}
            <a href="{{ post.redirect }}" target="_blank" rel="noopener noreferrer">{{ post.title }}</a>
          {% else %}
            <a href="{{ post.redirect | relative_url }}">{{ post.title }}</a>
          {% endif %}
        </h3>
        {% if preview_text != "" %}
          <p class="project-desc">{{ preview_text }}</p>
        {% endif %}
        <ul class="project-tags">
          <li>{{ post.date | date: '%B %d, %Y' }}</li>
          {% if post.external_source %}
            <li>{{ post.external_source }}</li>
          {% endif %}
        </ul>
      </div>
    {% endfor %}
  </div>

  {% if page.pagination.enabled %}
    {% include pagination.liquid %}
  {% endif %}
</div>
