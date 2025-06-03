---
layout: page
title: Library
permalink: /library/
---

<input type="text" id="search-box" placeholder="Search posts..." style="width: 100%; padding: 0.5rem; margin-bottom: 1rem;">

<div class="posts" id="search-results"></div>

<script>
  let postsData = [];

  fetch('/search.json')
    .then(response => response.json())
    .then(data => {
      postsData = data.sort((a, b) => new Date(b.date) - new Date(a.date));
      renderPosts(postsData.slice(0, 3)); // show 3 recent by default
    });

  const searchBox = document.getElementById('search-box');
  const searchResults = document.getElementById('search-results');

  searchBox.addEventListener('input', function () {
    const term = this.value.toLowerCase();
    if (term === '') {
      renderPosts(postsData.slice(0, 3));
      return;
    }
    const filtered = postsData.filter(post =>
      post.title.toLowerCase().includes(term) ||
      post.excerpt.toLowerCase().includes(term) ||
      post.content.toLowerCase().includes(term)
    );
    renderPosts(filtered);
  });

  function renderPosts(posts) {
    searchResults.innerHTML = '';
    if (posts.length === 0) {
      searchResults.innerHTML = '<p>No posts found.</p>';
      return;
    }
    posts.forEach(post => {
      const html = `
        <article>
          <h2><a href="${post.url}">${post.title}</a></h2>
          <p>${post.excerpt}</p>
          <a href="${post.url}">Read more</a>
        </article>
      `;
      searchResults.insertAdjacentHTML('beforeend', html);
    });
  }
</script>
