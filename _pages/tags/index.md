---
layout: null
permalink: /tags/
sitemap: false
---
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="robots" content="noindex">
    <meta http-equiv="refresh" content="0; url={{ '/categories/' | relative_url }}#tags">
    <title>Tags moved to Categories</title>
    <script>
      (function () {
        var tag = window.location.hash.replace(/^#/, '');
        var target = '{{ '/categories/' | relative_url }}' + (tag ? '#tag-' + tag : '#tags');
        window.location.replace(target);
      }());
    </script>
  </head>
  <body>
    <p>Tags have moved to <a href="{{ '/categories/' | relative_url }}#tags">Categories</a>.</p>
  </body>
</html>
