---
layout: page
title: Google Summer Of Code 2015
permalink: /gsoc2015/
---

![GSOC_LOGO](https://1-ps.googleusercontent.com/sxk/lUi00NOiZZtaYcm5-HDw_Ypz0k/s.google-melange.appspot.com/www.google-melange.com/soc/content/2-1-20150429/images/gsoc/logo/banner-gsoc2015.png.pagespeed.ce.1-XG35qq3RFCzwkXhRUG.png)

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
