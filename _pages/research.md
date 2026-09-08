---
layout: default
title: "Research"
permalink: /research/
author_profile: true
---

<div class="research-page research-index-page">
  <nav class="research-breadcrumb" aria-label="Breadcrumb">
    <a href="{{ '/' | relative_url }}" target="_self">Home</a>
    <span aria-hidden="true">›</span>
    <span aria-current="page">Research</span>
  </nav>

  <header class="research-index-hero">
    <p class="research-eyebrow">Research notebook</p>
    <h1>Research</h1>
    <p>A growing collection of questions, ideas, and thoughtful writing that inform my research.</p>
  </header>

  <div class="research-area-grid">
    {% for topic in site.data.research_topics %}
      {% assign topic_readings = site.data.research_readings[topic.id] %}
      {% assign topic_count = topic_readings | size %}
    <a class="research-area-card" href="{{ topic.url | relative_url }}" target="_self">
      <div class="research-area-card__top">
        <span class="research-area-card__number">{{ topic.number }}</span>
        <span class="research-area-card__count">{{ topic_count }} {% if topic_count == 1 %}reading{% else %}readings{% endif %}</span>
      </div>
      <p class="research-area-card__eyebrow">{{ topic.eyebrow }}</p>
      <h2>{{ topic.title }}</h2>
      <p class="research-area-card__description">{{ topic.description }}</p>
      <div class="research-tags" aria-label="Research topics">
        {% for tag in topic.tags %}<span>{{ tag }}</span>{% endfor %}
      </div>
      <span class="research-area-card__link">Explore reading list <i class="fas fa-arrow-right" aria-hidden="true"></i></span>
    </a>
    {% endfor %}
  </div>
</div>
