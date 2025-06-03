---
layout: page
title: Library
permalink: /library/
---

<input type="text" id="search-box" placeholder="Search posts..." style="width: 100%; padding: 0.5rem; margin-bottom: 1rem;" />

<div id="search-results"></div>

<script src="https://unpkg.com/lunr/lunr.js"></script>
<script>
  let idx = null;
  let posts = [];

  fetch('/search.json')
    .then(res => res.json())
    .then(data => {
      posts = data;
      idx = lunr(function () {
        this.ref('url');
        this.field('title');
        this.field('excerpt');
        this.field('content');
        data.forEach(doc => this.add(doc));
      });
    });

  document.getElementById('search-box').addEventListener('input', function () {
    const query = this.value;
    const results = idx.search(query);
    const container = document.getElementById('search-results');
    container.innerHTML = '';

    if (query.length < 2) return;

    results.forEach(result => {
      const post = posts.find(p => p.url === result.ref);
      const div = document.createElement('div');
      div.innerHTML = `<h3><a href="${post.url}">${post.title}</a></h3><p>${post.excerpt}</p>`;
      container.appendChild(div);
    });
  });
</script>
