---
layout: page
permalink: /contact/
title: contact
description: The ways to reach me.
nav: true
nav_order: 5
---

Email is the surest way to reach me — I read everything, and I answer most things.

<ul>
  <li><strong>Email</strong> — <a href="mailto:{{ site.data.socials.email }}">{{ site.data.socials.email }}</a></li>
  {% if site.data.socials.github_username %}<li><strong>GitHub</strong> — <a href="https://github.com/{{ site.data.socials.github_username }}">{{ site.data.socials.github_username }}</a></li>{% endif %}
  {% if site.data.socials.linkedin_username %}<li><strong>LinkedIn</strong> — <a href="https://www.linkedin.com/in/{{ site.data.socials.linkedin_username }}">{{ site.data.socials.linkedin_username }}</a></li>{% endif %}
  {% if site.data.socials.projecteuler_url %}<li><strong>Project Euler</strong> — <a href="{{ site.data.socials.projecteuler_url }}">profile</a></li>{% endif %}
  {% if site.data.socials.facebook_id %}<li><strong>Facebook</strong> — <a href="https://www.facebook.com/{{ site.data.socials.facebook_id }}">{{ site.data.socials.facebook_id }}</a></li>{% endif %}
  {% if site.data.socials.instagram_id %}<li><strong>Instagram</strong> — <a href="https://www.instagram.com/{{ site.data.socials.instagram_id }}">{{ site.data.socials.instagram_id }}</a></li>{% endif %}
  {% if site.data.socials.phone %}<li><strong>Phone</strong> — {{ site.data.socials.phone }}</li>{% endif %}
</ul>

<!-- Every line above is driven by _data/socials.yml: fill in a value there and the
     entry appears, delete it and the entry disappears. Nothing needs editing here. -->

If it is about work, the [CV](/cv/) and its [PDF](/cv.pdf) will save us both a round
trip. If it is about something I have built, [projects](/projects/) probably has the
long version. If it is a puzzle, lead with the puzzle.
