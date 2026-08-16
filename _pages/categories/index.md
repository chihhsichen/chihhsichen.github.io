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
    <nav class="categories-view-links" aria-label="Archive views">
      <a href="#folders" target="_self"><i class="fas fa-folder-open" aria-hidden="true"></i> By category</a>
      <a href="#tags" target="_self"><i class="fas fa-tags" aria-hidden="true"></i> By tag</a>
    </nav>
  </header>

  {% assign categories = site.categories | sort %}
  {% if categories.size > 0 %}
  <div class="category-collection" id="folders">
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
      <details class="category-folder" id="{{ category_name | slugify }}" open>
        <summary class="category-folder__summary">
          <span class="category-folder__icon" aria-hidden="true"><i class="fas fa-folder-open"></i></span>
          <span class="category-folder__heading">
            <span class="category-folder__title">{{ category_name }}</span>
            <span class="category-folder__meta">
              {% if child_category_count > 0 %}{{ child_category_count }} {% if child_category_count == 1 %}folder{% else %}folders{% endif %} · {% endif %}{{ primary_post_count }} {% if primary_post_count == 1 %}post{% else %}posts{% endif %}
            </span>
          </span>
          <span class="category-chevron" aria-hidden="true"></span>
        </summary>

        <div class="category-folder__body">
          {% if child_category_count > 0 %}
          <div class="subcategory-grid">
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

                  <details class="subcategory-card" id="{{ child_name | slugify }}">
                    <summary class="subcategory-card__summary">
                      <span class="subcategory-card__icon" aria-hidden="true"><i class="fas fa-folder"></i></span>
                      <span class="subcategory-card__heading">
                        <span class="subcategory-card__title">{{ child_name }}</span>
                        <span class="subcategory-card__meta">{{ child_post_count }} {% if child_post_count == 1 %}post{% else %}posts{% endif %}</span>
                      </span>
                      <span class="category-chevron" aria-hidden="true"></span>
                    </summary>

                    <div class="category-posts">
                      {% for child_post in category_posts %}
                        {% assign child_post_primary = child_post.categories | first %}
                        {% assign child_post_secondary = child_post.categories[1] %}
                        {% if child_post_primary == category_name and child_post_secondary == child_name %}
                        <a class="category-post" href="{{ child_post.url | relative_url }}">
                          <span class="category-post__title"><i class="fas fa-file-alt" aria-hidden="true"></i><span>{{ child_post.title }}</span></span>
                          <time datetime="{{ child_post.date | date_to_xmlschema }}">{{ child_post.date | date: "%b %d, %Y" }}</time>
                        </a>
                        {% endif %}
                      {% endfor %}
                    </div>
                  </details>
                {% endunless %}
              {% endif %}
            {% endfor %}
          </div>
          {% else %}
          <div class="category-posts category-posts--direct">
            {% for post in category_posts %}
              {% assign primary_name = post.categories | first %}
              {% if primary_name == category_name %}
              <a class="category-post" href="{{ post.url | relative_url }}">
                <span class="category-post__title"><i class="fas fa-file-alt" aria-hidden="true"></i><span>{{ post.title }}</span></span>
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

  {% assign tags = site.tags | sort %}
  {% if tags.size > 0 %}
  <section class="tag-explorer" id="tags" aria-labelledby="tags-title">
    <header class="tag-explorer__header">
      <div class="tag-explorer__icon" aria-hidden="true"><i class="fas fa-tags"></i></div>
      <div>
        <p class="tag-explorer__eyebrow">Explore across categories</p>
        <h2 id="tags-title">Browse by tag</h2>
        <p>Select a keyword to see its related posts.</p>
      </div>
    </header>

    <div class="tag-grid">
      {% for tag in tags %}
        {% assign tag_name = tag[0] %}
        {% assign tag_posts = tag[1] | sort: "date" | reverse %}
        <details class="tag-card" id="tag-{{ tag_name | slugify }}">
          <summary class="tag-card__summary">
            <span class="tag-card__hash" aria-hidden="true">#</span>
            <span class="tag-card__name">{{ tag_name }}</span>
            <span class="tag-card__count">{{ tag_posts.size }}</span>
            <span class="category-chevron" aria-hidden="true"></span>
          </summary>
          <div class="tag-card__posts">
            {% for post in tag_posts %}
            <a class="tag-card__post" href="{{ post.url | relative_url }}" target="_self">
              <span>{{ post.title }}</span>
              <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %d, %Y" }}</time>
            </a>
            {% endfor %}
          </div>
        </details>
      {% endfor %}
    </div>
  </section>
  {% endif %}
</div>

<style>
  .categories-page {
    --category-blue: #1f5fae;
    --category-ink: #26313d;
    --category-muted: #74808c;
    --category-line: #dce3ea;
    --category-soft: #f6f8fb;
    max-width: 920px;
    margin: 0 auto 4rem;
    color: var(--category-ink);
  }

  .categories-page .categories-breadcrumb {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    margin: 0.35rem 0 2.3rem;
    color: var(--category-muted);
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 0.9rem;
  }

  .categories-page .categories-breadcrumb a {
    color: var(--category-blue);
    text-decoration: none;
  }

  .categories-page .categories-breadcrumb a:hover {
    text-decoration: underline;
  }

  .categories-page .categories-header {
    margin-bottom: 1.7rem;
  }

  .categories-page .categories-header h1 {
    margin: 0;
    padding: 0;
    color: var(--category-ink);
    border: 0;
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: clamp(2rem, 4vw, 2.65rem);
    font-weight: 700;
    letter-spacing: -0.035em;
    line-height: 1.1;
  }

  .categories-page .categories-header p {
    margin: 0.65rem 0 0;
    color: var(--category-muted);
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 0.95rem;
  }

  .categories-page .categories-header .categories-header__eyebrow {
    margin-bottom: 0.45rem;
    color: var(--category-blue);
    font-size: 0.72rem;
    font-weight: 700;
    letter-spacing: 0.09em;
    text-transform: uppercase;
  }

  .categories-view-links {
    display: flex;
    gap: 0.5rem;
    margin-top: 1rem;
  }

  .categories-page .categories-view-links a {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    padding: 0.4rem 0.68rem;
    color: #5c6e80;
    border: 1px solid var(--category-line);
    border-radius: 8px;
    background: #fff;
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 0.7rem;
    text-decoration: none;
  }

  .categories-page .categories-view-links a:hover {
    color: var(--category-blue);
    border-color: #b9cbe0;
    background: #f6f9fd;
    text-decoration: none;
  }

  .category-collection {
    display: grid;
    gap: 1.25rem;
    scroll-margin-top: 5.5rem;
  }

  .category-folder {
    overflow: hidden;
    margin: 0;
    border: 1px solid var(--category-line);
    border-radius: 14px;
    background: #fff;
    box-shadow: 0 8px 24px rgba(39, 55, 72, 0.07);
  }

  .category-folder > summary,
  .subcategory-card > summary {
    list-style: none;
  }

  .category-folder > summary::-webkit-details-marker,
  .subcategory-card > summary::-webkit-details-marker {
    display: none;
  }

  .category-folder__summary {
    display: grid;
    grid-template-columns: 2.7rem minmax(0, 1fr) 0.8rem;
    align-items: center;
    gap: 0.9rem;
    min-height: 4.6rem;
    padding: 0.9rem 1.2rem;
    background: linear-gradient(135deg, #f8fbff 0%, #f3f6fa 100%);
    cursor: pointer;
  }

  .category-folder__summary:hover {
    background: #eef4fb;
  }

  .category-folder__summary:focus-visible,
  .subcategory-card__summary:focus-visible {
    outline: 3px solid rgba(31, 95, 174, 0.26);
    outline-offset: -3px;
  }

  .category-folder__icon {
    display: grid;
    width: 2.7rem;
    height: 2.7rem;
    place-items: center;
    border-radius: 10px;
    color: #fff;
    background: var(--category-blue);
    box-shadow: 0 5px 12px rgba(31, 95, 174, 0.2);
  }

  .category-folder__heading,
  .subcategory-card__heading {
    display: grid;
    min-width: 0;
    gap: 0.15rem;
  }

  .category-folder__title {
    color: var(--category-ink);
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 1.06rem;
    font-weight: 700;
    line-height: 1.35;
  }

  .category-folder__meta,
  .subcategory-card__meta {
    color: var(--category-muted);
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 0.76rem;
    line-height: 1.35;
  }

  .category-folder__body {
    padding: 1rem 1.2rem 1.2rem;
    border-top: 1px solid var(--category-line);
    background: var(--category-soft);
  }

  .subcategory-grid {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 0.8rem;
    align-items: start;
  }

  .subcategory-card {
    overflow: hidden;
    margin: 0;
    border: 1px solid var(--category-line);
    border-radius: 10px;
    background: #fff;
    transition: border-color 0.16s ease, box-shadow 0.16s ease;
  }

  .subcategory-card[open] {
    grid-column: 1 / -1;
    border-color: #bdcce0;
    box-shadow: 0 6px 16px rgba(39, 55, 72, 0.06);
  }

  .subcategory-card__summary {
    display: grid;
    grid-template-columns: 1.7rem minmax(0, 1fr) 0.7rem;
    align-items: center;
    gap: 0.7rem;
    min-height: 3.75rem;
    padding: 0.7rem 0.9rem;
    cursor: pointer;
  }

  .subcategory-card__summary:hover {
    background: #f8fafc;
  }

  .subcategory-card[open] > .subcategory-card__summary {
    background: #f5f8fc;
  }

  .subcategory-card__icon {
    color: #6c87a8;
    font-size: 1rem;
    text-align: center;
  }

  .subcategory-card__title {
    overflow-wrap: anywhere;
    color: var(--category-blue);
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 0.9rem;
    font-weight: 600;
    line-height: 1.35;
  }

  .category-chevron {
    width: 0.48rem;
    height: 0.48rem;
    border-right: 2px solid #8895a2;
    border-bottom: 2px solid #8895a2;
    transform: rotate(45deg) translate(-1px, -1px);
    transition: transform 0.18s ease;
  }

  details:not([open]) > summary .category-chevron {
    transform: rotate(-45deg);
  }

  .category-posts {
    border-top: 1px solid var(--category-line);
    background: #fff;
  }

  .category-posts--direct {
    overflow: hidden;
    border: 1px solid var(--category-line);
    border-radius: 10px;
  }

  .categories-page a.category-post {
    display: grid;
    grid-template-columns: minmax(0, 1fr) auto;
    align-items: center;
    gap: 1rem;
    min-height: 3.15rem;
    padding: 0.65rem 0.95rem;
    color: var(--category-ink);
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 0.84rem;
    line-height: 1.45;
    text-decoration: none;
  }

  .categories-page a.category-post + a.category-post {
    border-top: 1px solid #edf1f5;
  }

  .categories-page a.category-post:hover {
    color: var(--category-blue);
    background: #f8fafc;
    text-decoration: none;
  }

  .category-post__title {
    display: grid;
    grid-template-columns: 1rem minmax(0, 1fr);
    align-items: baseline;
    gap: 0.6rem;
    min-width: 0;
  }

  .category-post__title i {
    color: #a1acb8;
    font-size: 0.78rem;
  }

  .category-post time {
    color: #8a96a3;
    font-size: 0.74rem;
    white-space: nowrap;
  }

  .subcategory-card:target,
  .category-folder:target,
  .tag-card:target {
    box-shadow: 0 0 0 3px rgba(31, 95, 174, 0.17), 0 8px 24px rgba(39, 55, 72, 0.07);
  }

  .tag-explorer {
    margin-top: 3.5rem;
    scroll-margin-top: 5.5rem;
  }

  .tag-explorer__header {
    display: grid;
    grid-template-columns: 2.7rem minmax(0, 1fr);
    align-items: center;
    gap: 0.9rem;
    margin-bottom: 1rem;
    padding-bottom: 1rem;
    border-bottom: 1px solid var(--category-line);
  }

  .tag-explorer__icon {
    display: grid;
    width: 2.7rem;
    height: 2.7rem;
    place-items: center;
    color: var(--category-blue);
    border: 1px solid #cbd9e8;
    border-radius: 10px;
    background: #f4f8fd;
  }

  .categories-page .tag-explorer__eyebrow {
    margin: 0 0 0.18rem;
    color: var(--category-blue);
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 0.66rem;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .categories-page .tag-explorer h2 {
    margin: 0;
    padding: 0;
    color: var(--category-ink);
    border: 0;
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 1.25rem;
  }

  .categories-page .tag-explorer__header p:last-child {
    margin: 0.25rem 0 0;
    color: var(--category-muted);
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 0.76rem;
  }

  .tag-grid {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 0.65rem;
    align-items: start;
  }

  .tag-card {
    overflow: hidden;
    margin: 0;
    border: 1px solid var(--category-line);
    border-radius: 9px;
    background: #fff;
  }

  .tag-card[open] {
    grid-column: 1 / -1;
    border-color: #bdcce0;
  }

  .tag-card > summary {
    list-style: none;
  }

  .tag-card > summary::-webkit-details-marker {
    display: none;
  }

  .tag-card__summary {
    display: grid;
    grid-template-columns: 1rem minmax(0, 1fr) auto 0.65rem;
    align-items: center;
    gap: 0.5rem;
    min-height: 3rem;
    padding: 0.55rem 0.75rem;
    cursor: pointer;
  }

  .tag-card__summary:hover,
  .tag-card[open] > .tag-card__summary {
    background: #f7f9fc;
  }

  .tag-card__hash {
    color: #9aa8b6;
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-weight: 700;
  }

  .tag-card__name {
    overflow: hidden;
    color: #4c6075;
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 0.76rem;
    font-weight: 600;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .tag-card__count {
    display: grid;
    min-width: 1.5rem;
    height: 1.5rem;
    place-items: center;
    color: #68798a;
    border-radius: 999px;
    background: #edf2f7;
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 0.62rem;
  }

  .tag-card__posts {
    border-top: 1px solid var(--category-line);
    background: #fff;
  }

  .categories-page a.tag-card__post {
    display: grid;
    grid-template-columns: minmax(0, 1fr) auto;
    align-items: center;
    gap: 1rem;
    min-height: 2.9rem;
    padding: 0.6rem 0.85rem 0.6rem 2.25rem;
    color: var(--category-ink);
    font-family: "Avenir Next", Avenir, "Helvetica Neue", Arial, sans-serif;
    font-size: 0.76rem;
    text-decoration: none;
  }

  .categories-page a.tag-card__post + a.tag-card__post {
    border-top: 1px solid #edf1f5;
  }

  .categories-page a.tag-card__post:hover {
    color: var(--category-blue);
    background: #f8fafc;
    text-decoration: none;
  }

  .tag-card__post time {
    color: #8a96a3;
    font-size: 0.68rem;
    white-space: nowrap;
  }

  .categories-empty {
    padding: 2rem;
    border: 1px dashed var(--category-line);
    border-radius: 12px;
    color: var(--category-muted);
    text-align: center;
  }

  @media (max-width: 700px) {
    .categories-page .categories-breadcrumb {
      margin-bottom: 1.7rem;
    }

    .subcategory-grid {
      grid-template-columns: 1fr;
    }

    .subcategory-card[open] {
      grid-column: auto;
    }

    .tag-grid {
      grid-template-columns: 1fr;
    }

    .tag-card[open] {
      grid-column: auto;
    }

    .category-folder__summary {
      grid-template-columns: 2.35rem minmax(0, 1fr) 0.7rem;
      gap: 0.7rem;
      padding: 0.8rem 0.9rem;
    }

    .category-folder__icon {
      width: 2.35rem;
      height: 2.35rem;
    }

    .category-folder__body {
      padding: 0.75rem;
    }

    .categories-page a.category-post {
      display: block;
    }

    .category-post time {
      display: block;
      margin-top: 0.25rem;
      padding-left: 1.6rem;
    }

    .categories-page a.tag-card__post {
      display: block;
      padding-left: 1rem;
    }

    .tag-card__post time {
      display: block;
      margin-top: 0.2rem;
    }
  }
</style>

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
