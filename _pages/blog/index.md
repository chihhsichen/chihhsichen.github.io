---
layout: default
title: "Chih-Hsi Chen's Blog"
permalink: /blog/
author_profile: true
---

# 📝 Blog Posts

{% assign posts = site.posts %}
{% if posts.size > 0 %}
{% for post in posts %}

## [{{ post.title }}]({{ post.url | relative_url }})

**{{ post.date | date: "%B %d, %Y" }}**

{% if post.excerpt %}
{{ post.excerpt | strip_html | truncatewords: 50 }}
{% endif %}

[Read More →]({{ post.url | relative_url }})

---

{% endfor %}

{% else %}

No blog posts yet.

{% endif %}