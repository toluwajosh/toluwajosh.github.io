---
layout: page
permalink: /about/index.html
title: Joshua Owoyemi
tags: [Toluwaleke, Joshua, Owoyemi, Machine Learning]
imagefeature:
chart: true
---
<figure>
  <img src="{{ site.url }}/images/about_me_image.jpg" alt="Toluwaleke Joshua Owoyemi">
  <!-- <figcaption>Toluwaleke Joshua Owoyemi</figcaption> -->
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


My name is **Toluwaleke Joshua Owoyemi**, and this is my personal blog. I am a PhD student at the [Hashimoto-Kagami Laboratory](http://www.ic.is.tohoku.ac.jp/en/) of Tohoku University. My research is about application of machine learning to computer vision and robot manipulation. I am also interest in self-driving cars, so I am taking the [Udacity course](https://www.udacity.com/drive). In the past two years I've been learning a lot of things. I am currently learning web development, so this is like my test site.  Please follow my other channels and give a shoutout. Cheers.

<div class="social-icons">
        
        {% if site.owner.twitter %}
        <a href="http://twitter.com/{{ site.owner.twitter }}">
            <span class="fa-stack fa-lg">
                <i class="fa fa-circle fa-stack-2x fa-inverse"></i>
                <i class="fa fa-twitter fa-stack-1x"></i>
            </span>
        </a>
        {% endif %}
        {% if site.owner.google_plus %}
        <a href="{{ site.owner.google_plus }}">
            <span class="fa-stack fa-lg">
                <i class="fa fa-circle fa-stack-2x fa-inverse"></i>
                <i class="fa fa-google-plus fa-stack-1x"></i>
            </span>
        </a>
        {% endif %}
        {% if site.owner.instagram %}
        <a href="http://instagram.com/{{ site.owner.instagram }}">
            <span class="fa-stack fa-lg">
                <i class="fa fa-circle fa-stack-2x fa-inverse"></i>
                <i class="fa fa-instagram fa-stack-1x"></i>
            </span>
        </a>
        {% endif %}
        {% if site.owner.github %}
        <a href="http://github.com/{{ site.owner.github }}">
            <span class="fa-stack fa-lg">
                <i class="fa fa-circle fa-stack-2x fa-inverse"></i>
                <i class="fa fa-github fa-stack-1x"></i>
            </span>
        </a>
        {% endif %}
        {% if site.owner.facebook %}
        <a href="http://facebook.com/{{ site.owner.facebook }}">
            <span class="fa-stack fa-lg">
                <i class="fa fa-circle fa-stack-2x fa-inverse"></i>
                <i class="fa fa-facebook fa-stack-1x"></i>
            </span>
        </a>
        {% endif %}
    </div>