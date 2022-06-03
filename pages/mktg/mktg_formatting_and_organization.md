---
layout: default
permalink: /mktg/formatting-and-organization/
title: Formatting and Organization
parent: Marketers
audience: mktg
nav_order: 5
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

{% assign file = site.data.stylerules.formatting_and_organization %}
{% assign aud = page.audience %}

{% include get_rules_for_audience.md filename=file audience=aud %}