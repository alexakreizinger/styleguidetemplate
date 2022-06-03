---
layout: default
permalink: /all/grammar/
title: Grammar
parent: All
nav_exclude: true
search_exclude: true
audience: all
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

{% include get_all_rules.md filename=file %}