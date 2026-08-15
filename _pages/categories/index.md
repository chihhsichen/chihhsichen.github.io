---
layout: default
title: "Categories"
permalink: /categories/
author_profile: true
---

<div class="archive">
{% assign categories = site.categories | sort %}
{% if categories.size > 0 %}
  {% for category in categories %}
    {% assign cat_name = category[0] %}
    {% assign cat_posts = category[1] | sort: "date" | reverse %}
    <h2 id="{{ cat_name | slugify }}" class="archive__subtitle">{{ cat_name }} <small class="page__meta">({{ cat_posts.size }})</small></h2>
    {% for post in cat_posts %}
    <div class="list__item">
      <article class="archive__item">
        <h3 class="archive__item-title"><a href="{{ post.url | relative_url }}" rel="permalink">{{ post.title }}</a></h3>
        <p class="page__meta">{{ post.date | date: "%B %d, %Y" }}</p>
      </article>
    </div>
    {% endfor %}
  {% endfor %}
{% else %}
  <p>No categories yet.</p>
{% endif %}
</div>
