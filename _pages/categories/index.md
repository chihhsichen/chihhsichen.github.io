---
layout: default
title: "Categories"
permalink: /categories/
author_profile: true
---

<div class="categories-page">
  <nav class="categories-breadcrumb" aria-label="Breadcrumb">
    <a href="{{ '/' | relative_url }}">Home</a>
    <span aria-hidden="true">›</span>
    <span aria-current="page">Categories</span>
  </nav>

  <header class="categories-header">
    <p class="categories-header__eyebrow">Browse the archive</p>
    <h1>Categories</h1>
    <p>{{ site.posts.size }} posts, grouped by topic and course.</p>
  </header>

  {% assign categories = site.categories | sort %}
  {% if categories.size > 0 %}
  <div class="category-tree">
    {% for category in categories %}
      {% assign category_name = category[0] %}
      {% assign category_posts = category[1] | sort: "date" | reverse %}
      {% assign is_primary_category = false %}
      {% assign primary_post_count = 0 %}
      {% assign child_category_count = 0 %}
      {% assign counted_child_categories = '|' %}

      {% for post in category_posts %}
        {% assign primary_name = post.categories | first %}
        {% if primary_name == category_name %}
          {% assign is_primary_category = true %}
          {% assign primary_post_count = primary_post_count | plus: 1 %}
          {% assign child_name = post.categories[1] %}
          {% if child_name %}
            {% assign child_token = child_name | prepend: '|' | append: '|' %}
            {% unless counted_child_categories contains child_token %}
              {% assign counted_child_categories = counted_child_categories | append: child_name | append: '|' %}
              {% assign child_category_count = child_category_count | plus: 1 %}
            {% endunless %}
          {% endif %}
        {% endif %}
      {% endfor %}

      {% if is_primary_category %}
      <details class="category-tree__group" id="{{ category_name | slugify }}" open>
        <summary class="category-tree__row category-tree__row--primary">
          <span class="category-tree__icon" aria-hidden="true"><i class="fas fa-folder"></i></span>
          <span class="category-tree__name">{{ category_name }}</span>
          <span class="category-tree__count">
            {% if child_category_count > 0 %}{{ child_category_count }} {% if child_category_count == 1 %}category{% else %}categories{% endif %} · {% endif %}{{ primary_post_count }} {% if primary_post_count == 1 %}post{% else %}posts{% endif %}
          </span>
          <span class="category-tree__chevron" aria-hidden="true"></span>
        </summary>

        <div class="category-tree__children">
          {% if child_category_count > 0 %}
            {% assign rendered_child_categories = '|' %}
            {% for post in category_posts %}
              {% assign primary_name = post.categories | first %}
              {% assign child_name = post.categories[1] %}
              {% if primary_name == category_name and child_name %}
                {% assign child_token = child_name | prepend: '|' | append: '|' %}
                {% unless rendered_child_categories contains child_token %}
                  {% assign rendered_child_categories = rendered_child_categories | append: child_name | append: '|' %}
                  {% assign child_post_count = 0 %}
                  {% for child_post in category_posts %}
                    {% assign child_post_primary = child_post.categories | first %}
                    {% assign child_post_secondary = child_post.categories[1] %}
                    {% if child_post_primary == category_name and child_post_secondary == child_name %}
                      {% assign child_post_count = child_post_count | plus: 1 %}
                    {% endif %}
                  {% endfor %}

                  <details class="category-tree__child" id="{{ child_name | slugify }}">
                    <summary class="category-tree__row category-tree__row--child">
                      <span class="category-tree__icon" aria-hidden="true"><i class="fas fa-folder"></i></span>
                      <span class="category-tree__name">{{ child_name }}</span>
                      <span class="category-tree__count">{{ child_post_count }} {% if child_post_count == 1 %}post{% else %}posts{% endif %}</span>
                      <span class="category-tree__chevron" aria-hidden="true"></span>
                    </summary>
                    <div class="category-tree__posts">
                      {% for child_post in category_posts %}
                        {% assign child_post_primary = child_post.categories | first %}
                        {% assign child_post_secondary = child_post.categories[1] %}
                        {% if child_post_primary == category_name and child_post_secondary == child_name %}
                        <a class="category-tree__post" href="{{ child_post.url | relative_url }}">
                          <span>{{ child_post.title }}</span>
                          <time datetime="{{ child_post.date | date_to_xmlschema }}">{{ child_post.date | date: "%b %d, %Y" }}</time>
                        </a>
                        {% endif %}
                      {% endfor %}
                    </div>
                  </details>
                {% endunless %}
              {% endif %}
            {% endfor %}
          {% else %}
            <div class="category-tree__posts category-tree__posts--direct">
              {% for post in category_posts %}
                {% assign primary_name = post.categories | first %}
                {% if primary_name == category_name %}
                <a class="category-tree__post" href="{{ post.url | relative_url }}">
                  <span>{{ post.title }}</span>
                  <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %d, %Y" }}</time>
                </a>
                {% endif %}
              {% endfor %}
            </div>
          {% endif %}
        </div>
      </details>
      {% endif %}
    {% endfor %}
  </div>
  {% else %}
  <p class="categories-empty">No categories yet.</p>
  {% endif %}
</div>

<script>
  (function () {
    function openHashTarget() {
      if (!window.location.hash) return;
      var target = document.getElementById(window.location.hash.slice(1));
      if (!target) return;
      if (target.tagName === 'DETAILS') target.open = true;
      var parent = target.parentElement;
      while (parent) {
        if (parent.tagName === 'DETAILS') parent.open = true;
        parent = parent.parentElement;
      }
    }

    openHashTarget();
    window.addEventListener('hashchange', openHashTarget);
  }());
</script>
