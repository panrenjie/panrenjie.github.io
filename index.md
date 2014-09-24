---
layout: post
title: Welcome
author: shiny
category: site
tags: site
---

{{ page.title }}
================

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>