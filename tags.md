---
title: "Tags"
layout: page
---

A map of tags across notes.

{% comment %}
Construct a tag → notes mapping without plugins by scanning site.notes.
{% endcomment %}

{% assign tag_map = '{}' | split: '' %}
{% assign all_tags = '' | split: '' %}

{% for n in site.notes %}
  {% if n.tags %}
    {% for t in n.tags %}
      {% assign all_tags = all_tags | push: t %}
    {% endfor %}
  {% endif %}
{% endfor %}

{% assign unique_tags = all_tags | uniq | sort %}

{% if unique_tags.size > 0 %}
  <ul>
  {% for t in unique_tags %}
    <li id="{{ t | uri_escape }}"><strong>#{{ t }}</strong>
      <ul>
      {% for n in site.notes %}
        {% if n.tags and n.tags contains t %}
          <li><a href="{{ n.url | relative_url }}">{{ n.title }}</a></li>
        {% endif %}
      {% endfor %}
      </ul>
    </li>
  {% endfor %}
  </ul>
{% else %}
  <p>No tags yet. Add <code>tags: [something]</code> to your notes.</p>
{% endif %}
