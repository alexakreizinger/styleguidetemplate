---
layout: default
permalink: /dev/tone-and-content/
title: Tone and Content
parent: Developers
audience: dev
nav_order: 4
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

{% assign file = site.data.stylerules.tone_and_content %}
{% assign aud = page.audience %}

{% include get_rules_for_audience.md filename=file audience=aud %}