---
# This template is meant to demonstrate how the landing page for each audience should be formatted. This landing page will auto-generate a list of featured rules for the `dev` audience.

layout: default # Don't change this (unless you really want to, I guess).
permalink: /dev/ # This permalink should match the landing page's associated audience value: `/dev/`, `/tw/`, or `/mktg/`. Make sure to include the slashes before and after.
title: Developers # You can give the landing page any title you want, but the simplest option is to write out the name of the associated audience value. The value defined here will be important for maintaining the parent/child relationship between audience pages.
has_children: true # Don't change this. This how the theme generates parent/children page in the navigation sidebar.
has_toc: false # You can change this to `true` if you'd like to add a table of contents to the landing page, but I'd advise against it. It gets kind of cluttered and you don't really need one here.
search_exclude: true # You can change this to `true` if you'd like the landing page to show up in search results, but I'd also advise against it. The child pages (where the rules are actually hosted) ARE searchable, so making the landing page searchable just muddles the results with duplicate snippets.
audience: dev # This should match the landing page's associated audience value: `dev`, `tw`, or `mktg`.
nav_order: 3 # This value dictates the landing page's position on navigation sidebar. You can change this value to suit whatever page hierarchy you'd like. 
---
# {{page.title}} 

{% assign aud = page.audience %}

{::comment}
The following `assign`/`assign`/`capture` blocks use Liquid to assign values to variables that we'll need to auto-generate the pages. You should swap out these values with whatever makes sense for your specific configuration. For every ruleset YAML file you're pulling data from, you'll need three different Liquid statements:

{% assign <FILE> = site.data.stylerules.<NAME_OF_THE_FILE> %} - Assuming your rulesets are stored in `/_data/stylerules/`... but they should be. Also, don't include the `.yml` file extension here; it's not necessary.
{% assign  <SECTION> = "<SECTION TITLE>" %} - The value you include here will be displayed as an h3 header to group any featured rules from that file. However, that h3 syntax is automatically applied, so don't include the `###` markup here.
{% capture <LINK> %}{{site.baseurl}}{{page.permalink}}<SUBPAGE-URL-SLUG>/{% endcapture %} - The slug of the subpage where any featured rules should link to—but *not* including the audience value. For example, if you're pulling data from a punctuation ruleset, the subpage may have a slug of `/devs/punctuation`; you should only include the `punctuation/` part (note the slash at the end but not at the beginning).

The example below follows a `file1, file2...`/`section1, section2...`/`link1, link2...` naming convention for each variable. I suggest you do the same.
{:/comment}

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

{% assign file6 = site.data.stylerules.user_interfaces %}
{% assign section6 = "User interfaces" %}
{% capture link6 %}{{site.baseurl}}{{page.permalink}}user-interfaces/{% endcapture %}

{% assign file7 = site.data.stylerules.APIs_and_SDKs %}
{% assign section7 = "APIs and SDKs" %}
{% capture link7 %}{{site.baseurl}}{{page.permalink}}apis-and-sdks/{% endcapture %}

{::comment}
The following `include` blocks use Liquid to automatically pull any featured rules from their respective rulesets by using the variables that you assigned above. For each triad of ruleset variables you defined above (`FILE`, `SECTION`, and `LINK`), you'll need to incorporate all three of them into a single Liquid statement (note that `audience=aud` shouldn't change):

{% include get_featured_rules_for_audience.md filename=<FILE> audience=aud sectionname=<SECTION> sectionlink=<LINK> %}

The `---` dividers are an optional formatting choice; feel free to delete them or replace them with anything you'd like.
{:/comment}

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
---
{% include get_featured_rules_for_audience.md filename=file6 audience=aud sectionname=section6 sectionlink=link6 %}
---
{% include get_featured_rules_for_audience.md filename=file7 audience=aud sectionname=section7 sectionlink=link7 %}
