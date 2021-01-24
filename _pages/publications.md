---
layout: single
permalink: /publications
title: "Journal Publications"
excerpt: "Our pubs so far..."
last_modified_at: 2021-01-20
toc: true
sidebar:
  nav: "docs"
---

<table style="width:100%">

{% for pub in site.data.publications %}

  <tr>
    <td>
      <b>{{ pub.title }}</b>
      <a href="{{ pub.doi }}" class="btn" onclick="window.open(this.href, 'window', 'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;" title="DOI">
        <span> DOI</span>
      </a>
    </td>

  </tr>
{% endfor %}

</table>
