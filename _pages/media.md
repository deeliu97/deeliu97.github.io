---
layout: page
permalink: /media/
title: media
description: Interviews and coverage of my research in news media
nav: true
nav_order: 3
---

<!-- Media coverage page. Uses `_data/media.yml`. -->

<style>
/* Scoped styles for media table */
.media-table { width:100%; border-collapse:collapse; margin-top:1rem; }
.media-table th, .media-table td { text-align:left; padding:0.5rem 0.75rem; border-bottom:1px solid var(--muted-color,#e6e6e6); }
.media-table th { font-weight:700; color:var(--muted-color,#444); }
.media-table td a { color:var(--accent,#b16d6c); text-decoration:none; }
.media-note { color:#666; font-size:0.95rem; margin-top:0.75rem }
@media (max-width:640px){ .media-table thead{display:none} .media-table tr{display:block;margin-bottom:0.75rem} .media-table td{display:block;padding:0.35rem 0} }
</style>


{% assign items = site.data.media | sort: 'date' | reverse %}

{% if items and items.size > 0 %}
  <table class="media-table" aria-describedby="media-desc">
    <thead>
      <tr>
        <th>Date</th>
        <th>Venue</th>
        <th>Headline</th>
        <th></th>
      </tr>
    </thead>
    <tbody>
      {% for item in items %}
      <tr>
        <td>{{ item.date }}</td>
        <td>{{ item.venue }}</td>
        <td>{{ item.title }}</td>
        <td>
          {% if item.url %}
            <a href="{{ item.url }}" target="_blank" rel="noopener noreferrer">Read</a>
          {% endif %}
        </td>
      </tr>
      {% if item.note %}
      <tr><td colspan="4" class="media-note">{{ item.note }}</td></tr>
      {% endif %}
      {% endfor %}
    </tbody>
  </table>
{% else %}
  <p>No media items found yet — add entries to <code>_data/media.yml</code>.</p>
{% endif %}


