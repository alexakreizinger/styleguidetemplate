---
layout: default
permalink: /mktg/company-terminology/
title: Company Terminology
parent: Marketers
audience: mktg
nav_order: 1
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

{% assign file = site.data.stylerules.company_terminology %}
{% assign aud = page.audience %}

{% include get_rules_for_audience.md filename=file audience=aud %}