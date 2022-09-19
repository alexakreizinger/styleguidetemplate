---
layout: default
permalink: /mktg/ 
title: Marketers
has_children: true
has_toc: false
search_exclude: true
audience: mktg
nav_order: 4
---
# {{page.title}}

{% assign aud = page.audience %}

{% assign file1 = site.data.stylerules.company_terminology %}
{% assign section1 = "Company terminology" %}
{% capture link1 %}{{site.baseurl}}{{page.permalink}}company-terminology/{% endcapture %}

{% assign file2 = site.data.stylerules.grammar %}
{% assign section2 = "Grammar" %}
{% capture link2 %}{{site.baseurl}}{{page.permalink}}grammar/{% endcapture %}

{% assign file3 = site.data.stylerules.punctuation %}
{% assign section3 = "Punctuation" %}
{% capture link3 %}{{site.baseurl}}{{page.permalink}}punctuation/{% endcapture %}

{% assign file4 = site.data.stylerules.tone_and_content %}
{% assign section4 = "Tone and content" %}
{% capture link4 %}{{site.baseurl}}{{page.permalink}}tone-and-content/{% endcapture %}

{% assign file5 = site.data.stylerules.formatting_and_organization %}
{% assign section5 = "Formatting and organization" %}
{% capture link5 %}{{site.baseurl}}{{page.permalink}}formatting-and-organization/{% endcapture %}

## Quick tips
{% include get_featured_rules_for_audience.md filename=file1 audience=aud sectionname=section1 sectionlink=link1 %}

---

{% include get_featured_rules_for_audience.md filename=file2 audience=aud sectionname=section2 sectionlink=link2 %}

---

{% include get_featured_rules_for_audience.md filename=file3 audience=aud sectionname=section3 sectionlink=link3 %}

---

{% include get_featured_rules_for_audience.md filename=file4 audience=aud sectionname=section4 sectionlink=link4 %}

---

{% include get_featured_rules_for_audience.md filename=file5 audience=aud sectionname=section5 sectionlink=link5 %}