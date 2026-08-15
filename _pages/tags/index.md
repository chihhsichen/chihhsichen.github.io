---
layout: default
title: "Tags"
permalink: /tags/
author_profile: true
---

<div class="archive">
{% assign tags = site.tags | sort %}
{% if tags.size > 0 %}
  <p class="page__taxonomy">
    {% for tag in tags %}<a href="#{{ tag[0] | slugify }}" class="page__taxonomy-item">{{ tag[0] }} ({{ tag[1].size }})</a>{% endfor %}
  </p>
  {% for tag in tags %}
    {% assign tag_name = tag[0] %}
    {% assign tag_posts = tag[1] | sort: "date" | reverse %}
    <h2 id="{{ tag_name | slugify }}" class="archive__subtitle">{{ tag_name }} <small class="page__meta">({{ tag_posts.size }})</small></h2>
    {% for post in tag_posts %}
    <div class="list__item">
      <article class="archive__item">
        <h3 class="archive__item-title"><a href="{{ post.url | relative_url }}" rel="permalink">{{ post.title }}</a></h3>
        <p class="page__meta">{{ post.date | date: "%B %d, %Y" }}</p>
      </article>
    </div>
    {% endfor %}
  {% endfor %}
{% else %}
  <p>No tags yet.</p>
{% endif %}
</div>
