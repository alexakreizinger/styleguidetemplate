---
layout: default
permalink: /mktg/grammar/
title: Grammar
parent: Marketers
audience: mktg
nav_order: 2
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

{% assign file = site.data.stylerules.grammar %}
{% assign aud = page.audience %}

{% include get_rules_for_audience.md filename=file audience=aud %}