---
layout: single
classes: wide
permalink: /people
title: "People"
excerpt: "Our smart people."
---

<ul>
{% for member in site.data.members %}
  <li>
    <b>{{ member.name }}</b>
    <a href="https://www.linkedin.com/in/{{ member.linkedin }}"> LinkedIn </a> | 
    <a href="https://github.com/{{ member.github }}"> GitHub </a>
  </li>
{% endfor %}
</ul>
