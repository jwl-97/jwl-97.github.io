---
layout: default
title: "Algorithm"
project-header: true
---

<ul class="catalogue">
{% assign sorted = site.pages | sort: 'date' | reverse %}
{% for page in sorted %}
{% if page.algorithm == true %}
{% include post-list.html %}
{% endif %}
{% endfor %}
</ul>
