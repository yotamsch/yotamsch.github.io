---
layout: page
title: Tags
---
{% for tag in site.tags %}

  {% assign t = tag | first %}
  {% assign posts = tag | last %}

  <h3 id="tag-{{ t | downcase | replace:" ","-" }}">{{ t | upcase }} ({{ posts | size }})</h3>
  <ul class="tags">
  {% for post in posts %}
    {% if post.tags contains t %}
    <li itemscope>
        <a href="{{ site.github.url }}{{ post.url }}">{{ post.title }}</a>
        <p class="post-date"><span><i class="fa fa-calendar" aria-hidden="true"></i> {{ post.date | date: "%B %-d" }} - <i class="fa fa-clock-o" aria-hidden="true"></i> {% include read-time.html %}</span></p>
      </li>
    {% endif %}
  {% endfor %}
  </ul>
{% endfor %}
