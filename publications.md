---
title: Publications
permalink: /publications/
layout: page
excerpt: Papers I have published.
comments: false
---

{%- for post in site.publications -%}
  {%- capture current_year -%}{{ post.date | date: "%Y" }}{%- endcapture -%}
  {%- unless current_year == previous_year -%}
    <h2>{{ current_year }}</h2>
    {%- assign previous_year = current_year -%}
  {%- endunless -%}
  <article class="post-item">
    <h3 class="post-item-title" style="margin: auto 0">
      <b>{{ post.date | date: "%b. %d" }}</b> {% include text_divider.html %} <a href="{{ post.doi }}">{{ post.title | escape }}</a>
    </h3> 
    <img class="post-item-thumbnail" src="{{ post.image }}">
  </article>
{%- endfor -%}