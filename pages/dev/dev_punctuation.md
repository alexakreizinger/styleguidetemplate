---
layout: default
permalink: /dev/punctuation/
title: Punctuation
parent: Developers
audience: dev
nav_order: 3
---
# {{page.title}} 
{: .no_toc }
<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

{% assign file = site.data.stylerules.punctuation %}
{% assign aud = page.audience %}

{% include get_rules_for_audience.md filename=file audience=aud %}