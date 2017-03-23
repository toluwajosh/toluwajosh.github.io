---
layout: page
permalink: /about/index.html
title: Joshua Owoyemi
tags: [Toluwaleke, Joshua, Owoyemi, Machine Learning]
imagefeature:
chart: true
---
<figure>
  <img src="{{ site.url }}/images/avatar.jpg" alt="Toluwaleke Joshua Owoyemi">
  <figcaption>Toluwaleke Joshua Owoyemi</figcaption>
</figure>

{% assign total_words = 0 %}
{% assign total_readtime = 0 %}
{% assign featuredcount = 0 %}
{% assign statuscount = 0 %}

{% for post in site.posts %}
    {% assign post_words = post.content | strip_html | number_of_words %}
    {% assign readtime = post_words | append: '.0' | divided_by:200 %}
    {% assign total_words = total_words | plus: post_words %}
    {% assign total_readtime = total_readtime | plus: readtime %}
    {% if post.featured %}
    {% assign featuredcount = featuredcount | plus: 1 %}
    {% endif %}
{% endfor %}


My name is **Toluwaleke Joshua Owoyemi**, and this is my personal blog. I am currently learning web development, so this is like my test site. Check out my other channels at the footer of the page.