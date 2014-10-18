---
layout: page
title: "Dai Xi's Blog"
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
      <div>{{ post.description }}</div>
      <div>{{ post.content | more: "excerpt" }}</div>
      <div>
      {% unless post.tags == empty %}
            <span class="tag_box inline">
            {% assign tags_list = post.tags %}
            {% include JB/tags_list %}
            </span>
          {% endunless %} 
          </div>
          <br />
          <br />
      <div><a href="{{ BASE_PATH }}{{ post.url }}">阅读更多 >></a></div>
    </div>
    <hr />
  {% endfor %}
</ul>

