---
layout: page
title: Google Summer Of Code 2015
permalink: /gsoc2015/
---

![GSOC_LOGO](https://www.google-melange.com/archive/gsoc/2015/banner.png)

<div class="posts">
  {% for post in site.posts %}
    {% if post.categories contains 'gsoc' %}
      <article class="post">

        <h1><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h1>

        <div class="entry">
          {{ post.excerpt }}
        </div>

        <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Read More</a>
      </article>
    {% endif %}
  {% endfor %}
</div>
