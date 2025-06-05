---
layout: page
title: Library
permalink: /library/
header:
  image_fullwidth: bgheader.png
---

<input type="text" id="search-box" placeholder="Search posts..." style="width: 100%; padding: 0.5rem; margin-bottom: 1rem;">

<div class="posts" id="search-results">
  {% assign all_posts = site.posts %}
  {% for post in all_posts %}
    <article style="display: none;">
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p>{{ post.excerpt }}</p>
      <a href="{{ post.url }}">Read more</a>
    </article>
  {% endfor %}
</div>

<button id="load-more" style="margin-top: 1rem;">Show More</button>

<script>
  const searchBox = document.getElementById('search-box');
  const posts = Array.from(document.querySelectorAll('#search-results article'));
  const loadMoreBtn = document.getElementById('load-more');
  let visibleCount = 0;
  const batchSize = 10;

  function showNextBatch() {
    const nextBatch = posts.slice(visibleCount, visibleCount + batchSize);
    nextBatch.forEach(p => p.style.display = 'block');
    visibleCount += batchSize;
    if (visibleCount >= posts.length) loadMoreBtn.style.display = 'none';
  }

  searchBox.addEventListener('input', () => {
    const term = searchBox.value.toLowerCase().trim();
    posts.forEach(post => {
      const match = post.textContent.toLowerCase().includes(term);
      post.style.display = match ? 'block' : 'none';
    });
    if (term) {
      loadMoreBtn.style.display = 'none';
    } else {
      visibleCount = 0;
      posts.forEach(p => p.style.display = 'none');
      showNextBatch();
    }
  });

  loadMoreBtn.addEventListener('click', showNextBatch);

  // Show initial 10 posts
  showNextBatch();
</script>
