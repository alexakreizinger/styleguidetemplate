---
layout: default
permalink: /dev/user-interfaces/
title: User Interfaces
parent: Developers
audience: dev
nav_order: 6
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

{% assign file = site.data.stylerules.user_interfaces %}
{% assign aud = page.audience %}

{% include get_rules_for_audience.md filename=file audience=aud %}