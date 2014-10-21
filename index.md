---
layout: page
title: "Recent Posts"
tagline: 
---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
    <div>
      <h2><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h2>
      <div>
        <em>{{ post.date | date: "%Y-%m-%d" }}</em>      
      </div>
      <br />
      <div class="post-content-truncate">
        {% if post.content contains "<!--more-->" %}
          {{ post.content | split:"<!--more-->" | first % }}
          {% else %}
        {{ post.content | strip_html | truncatewords:100 }}
      {% endif %}
      </div>
      <div><a class="btn btn-primary" href="{{ BASE_PATH }}{{ post.url }}">阅读更多</a></div>
    </div>
    <hr />
  {% endfor %}
</ul>

