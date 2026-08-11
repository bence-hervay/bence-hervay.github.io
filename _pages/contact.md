---
layout: page
permalink: /contact/
title: contact
# SLOT — one line under the page title.
description:
nav: true
nav_order: 5
---

<!-- SLOT — a line or two about how you prefer to be reached. -->

[ to be written ]

<ul>
  {% if site.data.socials.email %}
    <li><strong>email</strong> — <a href="mailto:{{ site.data.socials.email }}">{{ site.data.socials.email }}</a></li>
  {% else %}
    <li><strong>email</strong> — [ to be supplied ]</li>
  {% endif %}
  {% if site.data.socials.github_username %}<li><strong>github</strong> — <a href="https://github.com/{{ site.data.socials.github_username }}">{{ site.data.socials.github_username }}</a></li>{% endif %}
  {% if site.data.socials.linkedin_username %}<li><strong>linkedin</strong> — <a href="https://www.linkedin.com/in/{{ site.data.socials.linkedin_username }}">{{ site.data.socials.linkedin_username }}</a></li>{% endif %}
  {% if site.data.socials.projecteuler_url %}<li><strong>project euler</strong> — <a href="{{ site.data.socials.projecteuler_url }}">profile</a></li>{% endif %}
  {% if site.data.socials.facebook_id %}<li><strong>facebook</strong> — <a href="https://www.facebook.com/{{ site.data.socials.facebook_id }}">{{ site.data.socials.facebook_id }}</a></li>{% endif %}
  {% if site.data.socials.instagram_id %}<li><strong>instagram</strong> — <a href="https://www.instagram.com/{{ site.data.socials.instagram_id }}">{{ site.data.socials.instagram_id }}</a></li>{% endif %}
  {% if site.data.socials.phone %}<li><strong>phone</strong> — {{ site.data.socials.phone }}</li>{% endif %}
</ul>

<!-- Every line above is driven by _data/socials.yml: fill a value in and the entry
     appears, leave it out and the entry disappears. Nothing to edit here. -->
