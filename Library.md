---
layout: page
title: Library
permalink: /library/
---

<div style="padding: 0 10%;">
  <div class="posts">
    {% for post in site.posts %}
      <article>
        <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
        <p>{{ post.excerpt }}</p>
      </article>
    {% endfor %}
  </div>
</div>

