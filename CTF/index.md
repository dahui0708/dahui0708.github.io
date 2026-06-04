---
layout: page
title: CTF
permalink: /ctf/
---

<div class="post-list">
{% assign ctf_posts = site.posts | where_exp: "post", "post.categories contains 'CTF'" %}

{% for post in ctf_posts %}
  <a class="card-wrapper" href="{{ post.url | relative_url }}">
    <div class="card post-preview flex-md-row-reverse">
      <div class="card-body d-flex flex-column">
        <h1 class="card-title my-2 mt-md-0">{{ post.title }}</h1>

        <div class="card-text content mt-0 mb-3">
          <p>{{ post.description | default: post.excerpt | strip_html | truncate: 160 }}</p>
        </div>

        <div class="post-meta flex-grow-1 d-flex align-items-end">
          <div class="me-auto">
            <i class="far fa-calendar fa-fw me-1"></i>
            <span>{{ post.date | date: "%b %-d, %Y" }}</span>
            <i class="far fa-folder-open fa-fw me-1 ms-3"></i>
            <span>{{ post.categories | join: ", " }}</span>
          </div>
        </div>
      </div>
    </div>
  </a>
{% endfor %}
</div>
