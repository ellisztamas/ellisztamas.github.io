---
title: "Posts"
permalink: /posts/
toc: false
---

I occasionally post about things people frequently ask me about.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>