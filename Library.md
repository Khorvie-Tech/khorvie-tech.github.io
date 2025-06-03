---
layout: page
title: Library
permalink: /library/
---

<input type="text" id="search-box" placeholder="Search posts..." style="width: 100%; padding: 0.5rem; margin-bottom: 1rem;">

<div class="posts" id="search-results">
  {% for post in site.posts %}
    <article>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p>{{ post.excerpt }}</p>
      <a href="{{ post.url }}">Read more</a>
    </article>
  {% endfor %}
</div>

<script>
  const searchBox = document.getElementById('search-box');
  const posts = Array.from(document.querySelectorAll('#search-results article'));

  searchBox.addEventListener('input', () => {
    const term = searchBox.value.toLowerCase();

    if(term === '') {
      posts.forEach(post => post.style.display = 'block');
      return;
    }

    posts.forEach(post => {
      const text = post.textContent.toLowerCase();
      post.style.display = text.includes(term) ? 'block' : 'none';
    });
  });
</script>
