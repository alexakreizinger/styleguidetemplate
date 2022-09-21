---
title: Home
layout: default
permalink: /
nav_order: 1
---
# AK's Style Guide Template
A Jekyll-based framework for building style guides that use single-sourced rulesets across multiple audiences, built by [Alexa Kreizinger](https://alexakreizinger.com/) and distributed under the GNU General Public License.

## Why this exists
Style guides are a must-have resource for any major organization—but what happens when you need to maintain multiple style guides for different audiences?

For example, guidelines that apply to someone designing a user interface might not apply to someone writing press releases, so it doesn’t make sense to enforce a single set of style rules for both. On the other hand, certain companywide styles certainly *will* apply to both audiences, and it can be tough to keep these rules in sync if they’re sourced from entirely separate guides.

This template strikes a balance between the need to maintain discrete rulesets for separate audiences and the need to unify certain overlapping rules that apply to multiple audiences. You may notice that certain style rules appear multiple times throughout this demo site, but each rule was only recorded in a single location. By using an audience-based tagging system, rules are automatically populated in any and all applicable sections (i.e., [Developers](https://alexakreizinger.github.io/styleguidetemplate/dev/), [Marketers](https://alexakreizinger.github.io/styleguidetemplate/mktg/), and/or [Technical Writers](https://alexakreizinger.github.io/styleguidetemplate/tw/)).

As such, if you ever need to update a rule, you’d only need to edit the YAML file where the rule is single-sourced instead of painstakingly combing through three separate sections where it could ostensibly appear.

## How it works
In a nutshell, this style guide template uses a combination of YAML files, Liquid variables, and Jekyll `include` tags to turn a collection of style rulesets into a mini database. Different pages of the style guide site can then draw upon this database to fetch relevant rules.

## Scalability
Although I designed this template to include three audiences, seven YAML ruleset files, and two audience-agnostic pages, none of these are fixed traits. You can scale your own style guide site to encompass as much content and as many audiences as you need—and, crucially, scaling your style guide won't require you to dismantle and rebuild any content you've already added.

## Further reading
For a more detailed overview of how everything works and how to get started, check out this template's [readme file](https://github.com/alexakreizinger/styleguidetemplate#aks-style-guide-template) on GitHub.