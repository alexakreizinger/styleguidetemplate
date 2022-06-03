---
layout: default
permalink: /tw/grammar/
title: Grammar
parent: Technical Writers
audience: tw
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