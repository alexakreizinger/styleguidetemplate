---
# This template is meant to demonstrate how audience-specific rule pages should be formatted. The example rule page outlined here will auto-generate all rules from the `punctuation.yml` file that have been tagged for the `dev` audience.

layout: default # Don't change this.
permalink: /dev/punctuation/ # This permalink is composed of two parts. The first part should match the landing page's associated audience value (`/dev/`, `/tw/`, or `/mktg/`), and the second part should be a short slug that describes the content of the page's ruleset (in this example, `punctuation/`). Make sure to include a slash before the audience value and after the page slug.
# Additionally, make sure the descriptive slug is consistent with the slug used for any other audiences that draw upon the same ruleset; for example, the equivalent page for technical writers should have a permalink of `/tw/punctuation/`. If you don't maintain this consistency, things will break!
title: Punctuation # You can give the landing page any title you want, but the simplest option is to write out the name of the ruleset.
parent: Developers # This value needs to match the `title` value for the audience's landing page; it's how the theme generates parent/children files in the navigation sidebar.
audience: dev # This should match the landing page's associated audience value: `dev`, `tw`, or `mktg`.
nav_order: 5 # This value dictates the landing page's position on navigation sidebar. You can change this value to suit the page hierarchy of your choosing.
# {{page.title}} 
---
# {{page.title}} 

{::comment}
The following block generates a collapsible table of contents for the page, which is collapsible by default. You're welcome to change or omit this however you'd like.
{:/comment}

{: .no_toc }
<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

{::comment}
The following `assign`/`assign`/`include` blocks are responsible for auto-generating all rules from the ruleset file. You'll need to change the first `assign` block to match the correct ruleset file:

{% assign file = site.data.stylerules.<NAME_OF_THE_FILE> %} - Assuming your rulesets are stored in `/_data/stylerules/`... but they should be. Also, don't include the `.yml` file extension here; it's not necessary.

Other than that, there's no additional changes to make or Liquid blocks to include. The `include` statement does all the work for you! That's why we bother with the hassle of formatting rules according to the YAML templates. ;)

{:/comment}

{% assign file = site.data.stylerules.punctuation %}
{% assign aud = page.audience %}

{% include get_rules_for_audience.md filename=file audience=aud %}