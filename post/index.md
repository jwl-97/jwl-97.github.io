---
layout: default
title: "Post"
description: 안드로이드 발표내용이나 관련 주제를 올려요.
project-header: true
---

<ul class="catalogue">
{% assign sorted = site.pages | sort: 'order' | reverse %}
{% for page in sorted %}
{% if page.post == true %}
{% include post-list.html %}
{% endif %}
{% endfor %}
</ul>
