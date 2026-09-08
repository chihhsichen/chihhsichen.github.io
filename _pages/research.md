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
    <div class="research-index-hero__label">
      <span>Research notebook</span>
      <span>Three areas of inquiry</span>
    </div>
    <h1>Ideas worth<br>returning to.</h1>
    <p>A curated home for the questions I study and the writing that continues to shape how I think.</p>
  </header>

  <div class="research-area-grid">
    {% for topic in site.data.research_topics %}
      {% assign topic_readings = site.data.research_readings[topic.id] %}
      {% assign topic_count = topic_readings | size %}
    <a class="research-area-card" href="{{ topic.url | relative_url }}" target="_self">
      <span class="research-area-card__orb" aria-hidden="true"></span>
      <div class="research-area-card__top">
        <span class="research-area-card__number">Area {{ topic.number }}</span>
        <span class="research-area-card__count">{{ topic_count }} {% if topic_count == 1 %}reading{% else %}readings{% endif %}</span>
      </div>
      <div class="research-area-card__body">
        <p class="research-area-card__eyebrow">{{ topic.eyebrow }}</p>
        <h2>{{ topic.title }}</h2>
        <p class="research-area-card__description">{{ topic.description }}</p>
      </div>
      <div class="research-area-card__footer">
        <div class="research-area-card__topics" aria-label="Research topics">
          {% for tag in topic.tags %}<span>{{ tag }}</span>{% endfor %}
        </div>
        <span class="research-area-card__arrow" aria-label="Explore {{ topic.title }}"><i class="fas fa-arrow-right" aria-hidden="true"></i></span>
      </div>
    </a>
    {% endfor %}
  </div>
</div>
