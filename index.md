---
title: Home
layout: default
permalink: /
nav_order: 1
render_with_liquid: false
---
# AK's Style Guide Template
A Jekyll-based style guide with single-sourcing across multiple audiences, built by [Alexa Kreizinger](https://alexakreizinger.com/).

Please note that various company names and product guidelines have been replaced with references to Aperture Science, a fictional organization from the *Portal* universe. Thank you for helping us help you help us all.

## Why this exists

Style guides an excellent, vital resource for any organization—but what happens when you need to maintain multiple style guides for different audiences?

Rules that apply to someone designing a user interface, for example, may not apply to someone writing press releases, so it doesn't make sense to use a single style guide for both. On the other hand, other rules certainly *will* apply to both audiences, and it can be tough to keep these rules in sync if they're sourced from entirely separate guides. 

This template strikes a balance between the need to maintain discrete rules for separate audiences with the need to unify rules that apply to one or more audiences. Although certain style rules appear multiple times throughout this guide, each rule was only recorded in a single location; by using a tagging system, each rule is automatically populated in the relevant sections for any applicable audience (i.e., [Developers](/dev), [Marketers](/mktg), and/or [Technical Writers](/tw). As such, if you ever need to edit or delete a rule, you only need to edit the rule's source file instead of painstakingly editing the three separate sections where it could possibly appear.

This template is also designed to be scalable, regardless of whether you have three audiences or thirty.

## How it works

TL;DR: A combination of YAML files, include tags, and Liquid variables that essentially turn your style ruleset into a mini database. (This is somehow both more complicated and less complicated than it sounds, but don't worry—I've already brute-forced my way through Jekyll's idiosyncrasies so you don't have to.)

### Style rules and YAML
Lists of style rules are stored in a series of YAML files in the [`_data/stylerules/`](https://github.com/alexakreizinger/styleguidetemplate/tree/main/_data/stylerules) directory. For example, a basic ruleset file called `punctuation.yml` might look like this:

```
description: Rules about punctuation.

rules:
- section: Semicolons
  topics:

  - rule: |
      ### Avoid overuse<br>
      Semicolons are your friend; however, like any friend, you might get sick of them if they show up too frequently. Tread carefully and wisely.
    audience: [tw, dev, mktg]

  - rule: |
      ### Clauses<br>
      You can use a semicolon to connect two independent clauses.
    examples:
      - |
        **Example:** The film received terrible reviews; none of the reviewers could even stay awake through the whole thing.
    audience: [tw, mktg]
```

There's a lot going on here, but the most important thing to note so far is the `audience` key. The first rule has the `tw`, `mktg`, and `dev` tags, corresponding to Technical Writers, Developers, and Marketers, respectively. The second rule, on the other hand, only applies to Technical Writers and Marketers.

Here's a slightly expanded example of the `punctuation.yml` ruleset file:

```
description: Rules about punctuation.

- section: Commas
  topics:

  - rule: |
      ### Clauses<br>
      If two independent clauses are separated by a coordinating conjunction, use a comma unless both clauses are very short.
    examples:
      - |
        **Long:** We built everything slowly over the course of several months, and it all seems to work so far.
      - |
        **Short:** We worked too quickly and it all fell apart.
    audience: [tw, mktg]

  - rule: |
      If a dependent clause and an independent clause are separated by a coordinating conjunction, don't use a comma unless the sentence would be unclear without it.
    examples:
      - |
        **Clear without comma:** The vacuum of space is cold and will kill you almost instantly. 
      - |
        **Needs comma for clarity:** Vacuums are unforgiving in space, but clean carpets marvelously well.
    audience: [tw, mktg]

  - rule: |
      ### Serial commas<br>
      Use serial commas (also known as *Oxford commas*).
    examples:
      - |
        **No:** I love my parents, Godzilla and Wonder Woman.
      - |
        **Yes:** I love my parents, Godzilla, and Wonder Woman.
    audience: [tw, dev, mktg]
    featured: |
      [Use serial commas.]({{site.baseurl}}{{page.permalink}}punctuation/#serial-commas)

rules:
- section: Semicolons
  topics:

  - rule: |
      ### Avoid overuse<br>
      Semicolons are your friend; however, like any friend, you might get sick of them if they show up too frequently. Tread carefully and wisely.
    audience: [tw, dev, mktg]

  - rule: |
      ### Clauses<br>
      You can use a semicolon to connect two independent clauses.
    examples:
      - |
        **Example:** The film received terrible reviews; none of the reviewers could even stay awake through the whole thing.
    audience: [tw, mktg]
```

Taken as a whole, this file creates a **Punctuation** ruleset with two sections: **Commas** and **Semicolons**. Each of these sections includes various rules.

Each rule has, at a minimum, the actual body of a rule and the audience to whom it applies. Some rules also have examples; other rules have a `featured` tag, which consists of a short blurb and a hyperlink, but the hyperlink uses Liquid tags to ensure that any fetched content is populated with the correct URL path.

### Include tags
There are several files in the `_includes` folder that contain Liquid loops to iterate over each rule file and pull the relevant information, depending on your needs.

[`get_all_rules.md`](https://github.com/alexakreizinger/styleguidetemplate/blob/main/_includes/get_all_rules.md) does exactly what it says—it fetches a list of all rules in a given YAML file, regardless of audience.

[`get_rules_for_audience.md`](https://github.com/alexakreizinger/styleguidetemplate/blob/main/_includes/get_rules_for_audience.md) accepts an `audience` variable and fetches a list of any rules in a given YAML file that are tagged with the provided audience. For example, you might want to fetch all rules that apply to Developers.

[`get_featured_rules_for_audience.md`](https://github.com/alexakreizinger/styleguidetemplate/blob/main/_includes/get_featured_rules_for_audience.md) accepts an `audience` variable and fetches a list of any featured rules in a given YAML file. These featured rules are displayed on an audience's landing page and include hyperlinks to the section where the featured rule resides.

### Audience pages

Each audience has a subfolder in the `pages` folder—for example, `pages/dev/` for Developers. Each audience subfolder includes a main landing page (which is where featured rules are displayed) and individual pages corresponding to the different YAML rulesets. These audience pages have no content, just Liquid variables and include tags.

### Putting it all together

So, for example, if you use the following Liquid tags in `pages/dev/dev_punctuation.md`, where `page.audience` is defined in the file's YAML frontmatter and has a value of `dev`:

```
{% assign file = site.data.stylerules.punctuation %}
{% assign aud = page.audience %}

{% include get_rules_for_audience.md filename=file audience=aud %}
```

You'd get a list of all punctuation rules that apply to the `dev` audience. Based on the expanded `punctuation.yml` file above, your output would look like this (but instead of in a code block it'd be correctly rendered in Markdown):

```
# Punctuation

Rules about punctuation.

## Commas

### Serial commas
Use serial commas (also known as *Oxford commas*).

* **No:** I love my parents, Godzilla and Wonder Woman.
* **Yes:** I love my parents, Godzilla, and Wonder Woman.

## Semicolons

### Avoid overuse
Semicolons are your friend; however, like any friend, you might get sick of them if they show up too frequently. Tread carefully and wisely.

```

Notice how only rules that had the `dev` tag showed up here? Instead of having to copy/paste them individually, we let Liquid do the heavy lifting for us. And if you were to repeat this process with a different YAML file or for a different audience tag, you'd get a completely different output from the same source files!