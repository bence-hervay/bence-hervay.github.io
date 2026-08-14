---
layout: page
permalink: /apps/
title: apps
# SLOT — one line under the page title.
description:
nav: true
nav_order: 3
# This page still lives and builds at /apps/ (a reverse proxy forwards
# apps.bence.io/* here); only the nav link target changes.
nav_external_url: https://apps.bence.io/
horizontal: false
---

<!-- SLOT — what this page is for, in your words. -->

[ to be written ]

<!-- Each card below is one file in _apps/. Copy any of them to add another. -->
<div class="projects">
{% assign sorted_apps = site.apps | sort: "importance" %}
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for app in sorted_apps %}
      {% include apps.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for app in sorted_apps %}
      {% include apps.liquid %}
    {% endfor %}
  </div>
  {% endif %}
</div>
