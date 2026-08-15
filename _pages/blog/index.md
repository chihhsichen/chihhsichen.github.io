---
layout: default
title: "Chih-Hsi Chen's Blog"
permalink: /blog/
author_profile: true
---

<div class="archive">
{% if paginator.posts.size > 0 %}
  {% for post in paginator.posts %}
  <div class="list__item">
    <article class="archive__item">
      <h2 class="archive__item-title"><a href="{{ post.url | relative_url }}" rel="permalink">{{ post.title }}</a></h2>
      <p class="page__meta">
        <i class="fa fa-fw fa-calendar" aria-hidden="true"></i> {{ post.date | date: "%B %d, %Y" }}
        {% if post.categories.size > 0 %}
          {% for cat in post.categories %}<a href="{{ '/categories/' | relative_url }}#{{ cat | slugify }}" class="page__taxonomy-item">{{ cat }}</a>{% endfor %}
        {% endif %}
      </p>
      {% if post.excerpt %}
      <p class="archive__item-excerpt">{{ post.excerpt | strip_html | truncatewords: 50 }}</p>
      {% endif %}
    </article>
  </div>
  {% endfor %}

  {% if paginator.total_pages > 1 %}
  <nav class="pagination">
    <ul>
      {% if paginator.previous_page %}
        <li><a href="{{ paginator.previous_page_path | relative_url }}" title="Previous Page">&laquo; Prev</a></li>
      {% else %}
        <li><a href="#" class="disabled">&laquo; Prev</a></li>
      {% endif %}
      {% for p in (1..paginator.total_pages) %}
        {% if p == paginator.page %}
          <li><a href="#" class="current">{{ p }}</a></li>
        {% elsif p == 1 %}
          <li><a href="{{ '/blog/' | relative_url }}">{{ p }}</a></li>
        {% else %}
          <li><a href="{{ site.paginate_path | replace: ':num', p | relative_url }}">{{ p }}</a></li>
        {% endif %}
      {% endfor %}
      {% if paginator.next_page %}
        <li><a href="{{ paginator.next_page_path | relative_url }}" title="Next Page">Next &raquo;</a></li>
      {% else %}
        <li><a href="#" class="disabled">Next &raquo;</a></li>
      {% endif %}
    </ul>
  </nav>
  {% endif %}
{% else %}
  <p>No blog posts yet.</p>
{% endif %}
</div>
