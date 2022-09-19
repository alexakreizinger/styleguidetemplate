# AK's Style Guide Template
A style guide template that uses YAML files to single-source style rules across multiple audiences. For an example of its output, check out the [demo site](https://alexakreizinger.github.io/styleguidetemplate/) generated from this repository. 

This template is a [Jekyll](https://jekyllrb.com/)-based framework that relies on vividh's [Liquify](https://github.com/vividh/liquify) plugin and the [Just the Docs](https://github.com/just-the-docs/just-the-docs) Jekyll theme (with some minor [customizations](#theming-and-site-customization)).

> :bulb: The actual style rules and other content included in this template are merely placeholders—you can (and should!) override them with your organization's unique style guidelines. For more information, see [Add your own content](#add-your-own-content).

## Table of contents
* [About](#about)
    * [Why this exists](#why-this-exists)
    * [How it works](#how-it-works)
    * [Style rules: YAML, Liquid, & you](#style-rules-yaml-liquid--you)
        * [Audiences](#audiences)
        * [Featured rules](#featured-rules)
    * [Scalability](#scalability)
* [Quickstart](#quickstart)
    * [Host with GitHub Pages](#host-with-github-pages)
    * [Preview your changes locally](#preview-your-changes-locally)
* [Add your own content](#add-your-own-content)
    * [Create and edit rules](#create-and-edit-rules)
        * [Add a new ruleset](#add-a-new-ruleset)
        * [Edit an existing ruleset](#edit-an-existing-ruleset)
    * [Create and edit pages](#create-and-edit-pages)
        * [Add a new audience landing page](#add-a-new-audience-landing-page)
        * [Add a new audience ruleset page](#add-a-new-audience-ruleset-page)
        * [Add a new audience-agnostic page](#add-a-new-audience-agnostic-page)
        * [Edit an existing page](#edit-an-existing-page)
    * [Create a new audience](#create-a-new-audience)
        * [Name your audience](#name-your-audience)
        * [Add new audience-specific pages](#add-new-audience-specific-pages)
        * [Add new audience tags to existing ruleset files](#add-new-audience-tags-to-existing-ruleset-files)
* [Directory structure](#directory-structure)
* [Theming and site customization](#theming-and-site-customization)
* [License](#license)
* [Contact](#contact)

## About
Different kinds of writing rely on different style conventions. That’s where this style guide template comes in—by segmenting a single set of rules into multiple discrete audiences, you can maintain a unified style within your organization *and* make it easy for writers of all stripes to find guidelines that are relevant to their needs. 

The [demo site](https://alexakreizinger.github.io/styleguidetemplate/) generated from this template includes the following pages:

* The [General Principles](https://alexakreizinger.github.io/styleguidetemplate/general/) page offers guidance for any and all writers.
* The [Developers](https://alexakreizinger.github.io/styleguidetemplate/dev/), [Marketers](https://alexakreizinger.github.io/styleguidetemplate/mktg/), and [Technical Writers](https://alexakreizinger.github.io/styleguidetemplate/tw/) pages contain comprehensive style rules tailored to developers, marketers, and technical writers, respectively. The content in these pages is single-sourced from a series of [YAML rulesets](#style-rules-yaml-liquid--you).
* The [Style Checklist](https://alexakreizinger.github.io/styleguidetemplate/checklist/) outlines core style rules to ensure that writers are publishing “minimum viable documentation.”

This demo site provides a basic framework that you can use to use to [set up the scaffolding](#quickstart) and subsequently [add your own content](#add-your-own-content). Additionally, since this template was designed to be [scalable](#scalability), you can incorporate as many pages or audiences as you'd like.

### Why this exists
Style guides are a must-have resource for any major organization—but what happens when you need to maintain multiple style guides for different audiences?

For example, guidelines that apply to someone designing a user interface might not apply to someone writing press releases, so it doesn’t make sense to enforce a single set of style rules for both. On the other hand, other companywide styles certainly *will* apply to both audiences, and it can be tough to keep these rules in sync if they’re sourced from entirely separate guides.

This template strikes a balance between the need to maintain discrete rulesets for separate audiences and the need to unify certain overlapping rules that apply to multiple audiences. If you browse the [demo site](https://alexakreizinger.github.io/styleguidetemplate/) generated from this repository, you may notice that certain style rules appear multiple times throughout the guide, but each rule was only recorded in a single location. By using an audience-based tagging system, rules are automatically populated in any and all applicable sections (i.e., [Developers](https://alexakreizinger.github.io/styleguidetemplate/dev/), [Marketers](https://alexakreizinger.github.io/styleguidetemplate/mktg/), and/or [Technical Writers](https://alexakreizinger.github.io/styleguidetemplate/tw/)).

As such, if you ever need to update a rule, you’d only need to edit the YAML file where the rule is single-sourced instead of painstakingly combing through three separate sections where it could ostensibly appear.

### How it works
In a nutshell, this style guide template uses a combination of YAML files, Liquid variables, and Jekyll `include` tags to turn a collection of style rulesets into a mini database. Different pages of the style guide site can then draw upon this database to fetch relevant rules.

The sequence of events is essentially as follows:

1. Style rules are stored in a YAML file in the `/_data/stylerules/` folder. For example, a basic ruleset file called `punctuation.yml` might contain fifteen discrete rules. Each rule in this file is stored as a set of key-value pairs—hence "mini database"—including an `audience` key that specifies which audiences the rule applies.

2. Several Markdown files in the `/_includes/` folder each contain different Liquid statements that tell Jekyll to fetch rules from the YAML ruleset file. For example, `get_rules_for_audience.md` is a series of statements that, when evaluated, will fetch all rules that apply to a particular audience but omit any rules that don't apply. 

3. On the site page where the rules need to be displayed, you can use an `include` tag to call one of the "function" files mentioned in Step 2. You'll need to pass variables to the `include` tag—for example, if you'd like to fetch all rules from `punctuation.yml` that apply to the `dev` (Developers) audience, your `include` tag might look like this:
<br>`{% include get_rules_for_audience.md filename='site.data.stylerules.punctuation.yml' audience='dev' %}`
<br>Let's assume that only nine of the fifteen rules included in that YAML file apply to the Developers audience. By using that simple `include` tag on a Developers-specific page, you can automatically fetch all nine of those rules and display them with a single line of code!

In practice, the process of using `include` tags to display content on pages is a *bit* more involved than the example above... but not by much. If you'd like to see `include` tags in action, check out [`audience_landing_page_template.md`](/_templates/audience_landing_page.template.md) and [`audience_rule_page_template.md`](/_templates/audience_rule_page_template.md).

### Style rules: YAML, Liquid, & you
As illustrated by the previous section, everything about this template ultimately goes back to those YAML ruleset files (located in `/_data/stylerules/`), so it's crucial that these files are formatted correctly.

And yes, working with YAML can be a bit tricky at times (so many indents! so much whitespace!), but the upsides here are twofold: (1) since Liquid does the heavy lifting and fetches rules automatically, these YAML rulesets are usually the only thing you'll need to edit whenever you need to add/update/remove rules; and (2) when you update a rule in the YAML file, you'll only need to update the rule one time rather than multiple times for multiple audiences.

If you'd like to learn more about how YAML ruleset files are formatted (and why), check out [`rule_template_generic.yml`](/_templates/rule_template_generic.yml) and [`rule_template_with_example.yml`](/_templates/rule_template_with_examples.yml).

#### Audiences

Every rule in the YAML ruleset files has an `audience` key. This key can have one or more values; each value specifies the audience(s) to whom that rule applies.

For example, if a rule applies to the Marketers and Technical Writers audiences, its `audience` key-value pair would look like this:

```
  - rule: |
      ### Contractions<br>
      It's okay to use contractions. 
    audience: [tw, mktg]
```

Currently, this template has three audiences, but you could [scale](#scalability) your own style guide site incorporate five or ten or even thirty audiences. The three default audiences are:

* [Developers](https://alexakreizinger.github.io/styleguidetemplate/dev/) (`dev`)
* [Marketers](https://alexakreizinger.github.io/styleguidetemplate/mktg/) (`mktg`)
* [Technical Writers](https://alexakreizinger.github.io/styleguidetemplate/tw/) (`tw`)

Each audience corresponds to a designated section of the demo site; all other pages outside these sections (such as [General Principles](https://alexakreizinger.github.io/styleguidetemplate/general/)) are audience-neutral. Each audience section has its own landing page, which displays a list of ["featured" rules](#featured-rules) for that audience, as well as a number of subpages to display rules fetched from YAML ruleset files. Each subpage corresponds to a single YAML ruleset file.

> :bulb: If a given YAML ruleset file doesn't have any rules that apply to a given audience, there's no point in having an audience subpage that corresponds to that ruleset. 
<br>For example, since none of the rules in `APIs_and_SDKs.yml` apply to Marketers (and probably never will, given the subject matter), the Marketers section of the demo site doesn't have an "APIs and SDKs" page—if I did include that page, it would be blank!

For example, the Developers section of the demo site has a *Developers* landing page, as well as subpages for *Company Terminology*, *Grammar*, *Punctuation*, *Tone and Content*, *Formatting and Organization*, *User Interfaces*, and *APIs and SDKs*. 

Even though the Technical Writers section of the demo site also has a *Grammar* subpage, the *Developers > Grammar* subpage and the *Technical Writers > Grammar* subpage aren't identical. Many rules between them overlap, but they're fetching rules based on different `audience` values, which means that rules that apply to one audience may not apply to the other (and vice versa).

For a more detailed overview of how audience pages are formatted, check out [`audience_landing_page_template.md`](/_templates/audience_landing_page.template.md) and [`audience_rule_page_template.md`](/_templates/audience_rule_page_template.md).

#### Featured rules

Some items in the YAML ruleset files have a `featured` key. The `get_featured_rules_for_audience` file looks for rules that have this `featured` key and displays the `featured` value accordingly; rules without a `featured` key will be skipped over entirely. 

Featured rules are displayed as a list of "quick tips" on each audience's landing page and are designed to link back to the subpage/section from which each featured rule originates. The `featured` key's value should consist of a short blurb that summarizes the rule and a hyperlink to the main rule; this hyperlink uses Liquid tags to ensure that any fetched content is populated with the correct URL path.

For example, a rule in `grammar.yml` contains the following content:

```
- rule: |
      ### Second-person pronouns<br>
      When addressing the reader, it's okay to use second-person pronouns like *you* and *your.* Don't use third-person language like *user* or *customer* in public-facing materials written for those very same users and customers—address them directly instead!
    audience: [tw, dev]
    featured: |
      [Use second-person pronouns like *you* and *your* to address the reader.]({{site.baseurl}}{{page.permalink}}grammar/#second-person-pronouns)
```

When rendered in the destination page, `{{site.baseurl}}` and `{{page.permalink}}` will be replaced with their respective values. So if you call `get_featured_rules_for_audience.md` on the Developers landing page, the following Markdown is rendered:

` [Use second-person pronouns like *you* and *your* to address the reader.](alexakreizinger.github.io/styleguidetemplate/devs/grammar/#second-person-pronouns) `

Since this rule originated from `grammar.yml`, it includes a hyperlink from the Developers landing page to the Developer-specific *Grammar* page—and it even links directly to the *Second-person pronouns* heading! However, if you call `get_featured_rules_for_audience.md` on the Technical Writers landing page, it'll generate a link to the Technical Writing-specific *Grammar* page instead. 

Note that in the example above, both the `tw` and `dev` audiences will count this rule as a "featured" rule. Rules that are features for one audience will be featured for all other audiences to whom that rule applies.

> :bulb: To ensure that audience landing pages are formatted correctly, make sure that every ruleset has at least one featured rule that applies to each audience (unless, like in the Marketers example above, the ruleset doesn't have any applicable rules for that audience at all). However, as a rule of thumb, try to include anywhere from three to ten featured rules per audience per ruleset.

For a more detailed overview of how and when to use featured rules, check out [`audience_landing_page_template.md`](/_templates/audience_landing_page.template.md) and [`rule_template_with_examples.yml`](/_templates/rule_template_with_examples.yml).

### Scalability
Although I designed this template to include three [audiences](#audiences), seven [YAML ruleset files], and two audience-agnostic pages ([General Principles](https://alexakreizinger.github.io/styleguidetemplate/general/) and [Style Checklist](https://alexakreizinger.github.io/styleguidetemplate/checklist/)), none of these are fixed traits. You can scale your own style guide site to encompass as much content and as many audiences as you need—and, crucially, scaling your style guide won't require you to dismantle and rebuild any content you've already added.

For more information, see [Create and edit rules](#create-and-edit-rules), [Create and edit pages](#create-and-edit-pages), and [Create a new audience](#create-a-new-audience).

([return to table of contents](#table-of-contents))

## Quickstart
To build the foundation for your own style guide site in GitHub:

1. [Create a new repository](https://github.com/alexakreizinger/styleguidetemplate/generate) from this template.
<br>(Some of the files in this repository won't be necessary for your own style guide site. For more information about the which files in this template are safe to delete or modify, refer to [Directory structure](#directory-structure).)

2. In your repo's `_config.yml` file, modify the key-value pairs shown below.
<br>(These are the minimum keys you must modify to make your style guide site work correctly, but you can edit any other key-value pairs you see fit. Consult Jekyll's [Configration Options](https://jekyllrb.com/docs/configuration/options/) documentation for basic information and Just the Docs' [Configuration](https://just-the-docs.github.io/just-the-docs/docs/configuration/) guide for theme-specific options.)

```
title: <the title of your site>
description: <the description for your site>
url: <the top-level domain of your site (e.g., "https://username.github.io")>
baseurl: <the baseurl of your site, often the same name as your repo (e.g., "/styleguide")>
```

3. If you'd like to use GitHub Pages to host your style guide site, see [Host with GitHub Pages](#host-with-github-pages) below. 

These steps will provide you with a functional style guide site. However, you'll still need to customize the content of your site to override the template's placeholder content. To learn more, see [Add your own content](#add-your-own-content).

### Host with GitHub Pages
Since GitHub Pages normally can't build sites that use [unsupported plugins](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#plugins) (like the [Liquify](https://github.com/vividh/liquify) plugin, which this template can't function without), this template's demo site uses a custom [GitHub Actions workflow](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions) as a workaround. This `build-jekyll.yml` workflow file is stored in the `/.github/workflows/` folder.

If you'd like to host your own style guide site with GitHub Pages, make sure not to delete that workflow file. Additionally, you'll need to set up your style guide repository to have two branches—`main` and `gh-pages`—and configure GitHub Pages to build from the `gh-pages` branch. The workflow then functions as follows:

* Every time a change is pushed to `main`, the custom action automatically uses the files in `main` to build website assets in `gh-pages`.
* GitHub Pages detects the changes in `gh-pages` and automatically generates a new version of your website from these latest assets.
* Changes are pushed to your live style guide site.

> :warning: Don't directly edit any files in the `gh-pages` branch; when the `build-jekyll.yml` workflow runs, it overwrites the entire `gh-pages` branch. You should only make commits to `main`.

### Preview your changes locally
Although you technically don't need to install Jekyll to use this template, it's often helpful to build a staging site locally to preview your changes before opening a pull request. To preview your changes:

1. [Install Jekyll](https://jekyllrb.com/docs/installation/).
2. Clone the `main` branch of your style guide repo.
3. In the command-line interface of your choosing, open the directory where you saved the local copy of your repo and run `bundle exec jekyll serve`.
4. In the web browser of your choosing, navigate to the server address displayed in the command line's output.

As you edit the local files in your cloned repo, you'll be able to view updates in the Jekyll staging site in (almost) real time. If everything looks good in the staging site, it's probably safe to push those changes to `main`.

([return to table of contents](#table-of-contents))

## Add your own content
After you've [set up the scaffolding](#quickstart) for your style guide site, you can start adding your organization's specific style rules and overriding the placeholder content included in this template. 

### Create and edit rules

#### Add a new ruleset
To add an entirely new ruleset file:

1. Create a new YAML file in `_data/stylerules/`. (You can use [`rule_template_generic.yml`](/_templates/rule_template_generic.yml) as a base.)
2. Add content to your ruleset file.
3. For any audiences to whom this ruleset is applicable, add the necessary Liquid blocks to add [featured rules](#featured-rules) to that audience's landing page. (See [`audience_landing_page_template.md`](/_templates/audience_landing_page.template.md) for guidance.)
4. For any audiences to whom this ruleset is applicable, [add a new audience ruleset page](#add-a-new-audience-ruleset-page) for that ruleset.

#### Edit an existing ruleset
To edit an existing ruleset:

1. Find the applicable YAML file in `_data/stylerules/`. 
2. Add, edit, or delete rules as needed. (See [`rule_template_generic.yml`](/_templates/rule_template_generic.yml) and [`rule_template_with_examples.yml`](/_templates/rule_template_with_examples.yml) for guidance.)

There's no need to edit the audience pages where these rulesets appear; if everything is configured correctly, the changes you make to a ruleset file will automatically be reflected in any applicable pages. 

### Create and edit pages

#### Add a new audience landing page

1. Create a new Markdown file in the folder for the applicable audience. (You can use [`audience_landing_page_template.md`](/_templates/audience_landing_page.template.md) as a base.)
2. Modify the following keys in the page's [front matter](https://jekyllrb.com/docs/front-matter/):
* `permalink`
* `title`
* `audience`
* `nav_order`
3. Modify the page's Liquid blocks to pull [featured rules](#featured-rules) from any ruleset files that are applicable for that audience.

For an example of an audience landing page, see the [Developers](https://alexakreizinger.github.io/styleguidetemplate/dev/) page of the demo site.

#### Add a new audience ruleset page

1. Create a new Markdown file in the folder for the applicable audience. (You can use [`audience_rule_page_template.md`](/_templates/audience_rule_page_template.md) as a base.)
2. Modify the following keys in the page's [front matter](https://jekyllrb.com/docs/front-matter/):
* `permalink`
* `title`
* `parent`
* `audience`
* `nav_order`
3. Modify the page's Liquid blocks to generate a list of rules from the ruleset file of your choosing.

For an example of an audience ruleset page, see the [Developers > Punctuation](https://alexakreizinger.github.io/styleguidetemplate/dev/punctuation/) page of the demo site.

#### Add a new audience-agnostic page

1. Create a new Markdown file in `/pages/`.
2. Make sure to include the following keys in the page's [front matter](https://jekyllrb.com/docs/front-matter/):
* `layout` (value should be `default`)
* `permalink`
* `title`
* `nav_order` (if you'd like the page to be accessible in the navigation bar) or `nav_exclude` (if you'd like the page to be hidden from the navigation bar)
3. Add content as you see fit.

For an example of an audience-agnostic page, see the [General Principles](https://alexakreizinger.github.io/styleguidetemplate/general/) page of the demo site.

#### Edit an existing page

Under most circumstances, you shouldn't edit audience landing pages or audience ruleset pages directly. However:

* If you'd like to edit the content that appears on an audience page, [edit any applicable ruleset file(s)](#edit-an-existing-ruleset).
* If you'd like to modify an audience page's title, permalink, or location in the navigation bar, edit that page's [front matter](https://jekyllrb.com/docs/front-matter/).
* If your Liquid formatting isn't working properly and you *do* need to edit an audience page directly, consult [`audience_landing_page_template.md`](/_templates/audience_landing_page.template.md) and [`audience_rule_page_template.md`](/_templates/audience_rule_page_template.md) for guidance.

On the other hand, audience-agnostic pages (like [`general_principles.md`](/pages/general_principles.md)) don't use single-sourced data; you can edit these pages directly without issue.

### Create a new audience

#### Name your audience

* Choose a simple "codename" for your audience. You'll need to use this value in audience page permalinks and ruleset audience tags, so choose a name that's short and memorable. For example, if you'd like to add a UX Designers audience, you might choose to use an audience value of `ux` in permalinks and audience tags.

#### Add new audience-specific pages 

1. Create a folder for your audience in `/pages/`.
2. In this folder, [create a landing page](#add-a-new-audience-landing-page) for your audience.
3. In this folder, [create a ruleset page](#add-a-new-audience-ruleset-page) for each ruleset that applies to your audience.

#### Add new audience tags to existing ruleset files

1. Decide which rulesets (if any) in `_data/stylerules` are relevant to your audience.
2. [Edit existing ruleset files](#edit-an-existing-ruleset) to add new tags (using the [audience name](#name-your-audience) you chose earlier) to all of the existing rules that apply to your audience. <br>For example, a rule that currently has the key-value pair `audience: [tw, dev]` would be changed to `audience: [tw, dev, ux]`.

([return to table of contents](#table-of-contents))

## Directory structure
The following outline describes the purpose of each file in this template repo and whether (and when) you should modify it. 

<details>
  <summary>Files in the <b><code>styleguidetemplate</code> repo</b></summary>

* [`/.github/workflows/build-jekyll.yml`](/.github/workflows/build-jekyll.yml): A custom GitHub Actions workflow to deploy the demo site to GitHub Pages. For more information, see [Host with GitHub Pages](#host-with-github-pages).
  
* [`/_data/stylerules/`](/_data/stylerules/): A folder that contains the various YAML rulesets that comprise the content of the demo site. If you're creating your own style guide, you can edit and override these rulesets as you see fit. For more information, see [Style rules, YAML, Liquid, & you](#style-rules-yaml-liquid--you) and [Create and edit rules](#create-and-edit-rules).

* [`/_includes/`](/_includes/): A folder that contains several files that use Liquid tags to fetch style rules from their respective YAML data files. For more information, see the [How it works](#how-it-works) section of this readme and Jekyll's [Includes](https://jekyllrb.com/docs/includes/) documentation.
<br>**NOTE:** Modifying the files in this folder will likely break your entire style guide site. Edit at your own risk!

    * [`get_all_rules.md`](/_includes/get_all_rules.md): Fetches all rules from a given ruleset YAML file, regardless of audience.

    * [`get_featured_rules_for_audience.md)`](/_includes/get_featured_rules_for_audience.md): For a specified audience, fetches any "featured" rules from a given YAML ruleset that have been tagged with that audience. For example, you can fetch all featured rules with the `dev` audience tag. For more information, see [Audiences](#audiences) and [Featured rules](#featured-rules).

    * [`get_rules_for_audience.md`](/_includes/get_rules_for_audience.md): For a specified audience, fetches any rules from a given ruleset YAML file that have been tagged with that audience. For example, you can fetch all rules with the `dev` audience tag. For more information, see [Audiences](#audiences).

* [`/_plugins/`](/_plugins/): This folder contains the [Liquify](https://github.com/vividh/liquify) plugin, which this template depends upon to properly generate pages. Don't edit or delete the Liquify plugin, but you're welcome to add other plugins to this folder as needed.

* [`/_sass/`](/_sass/): A folder that contains the .scss files used to customize the Just the Docs site theme. You can edit or delete these files to suit your own needs. For more information, see [Theming and site customization](#theming-and-site-customization).

* [`/_templates/`](/_templates/): Various files that you can use as a base for creating new pages and files within the broader style guide template; you can also use them as explainers to help you edit exiting pages and files. 

    * [`audience_landing_page_template.md`](/_templates/audience_landing_page.template.md): A template for an audience landing page (e.g., `/devs/`). This file is heavily annotated to provide an in-depth explanation of how landing pages work.

    * [`audience_rule_page_template.md`](/_templates/audience_rule_page_template.md): A template for an audience rule page (e.g., `/devs/punctuation/`). This file is heavily annotated to provide an in-depth explanation of how rule pages work.

    * [`rule_template_generic.yml`](/_templates/rule_template_generic.yml): A template for the YAML rulesets included in `/_data/stylerules/`. This file was designed as a bare-bones structural template that you can quickly copy/paste to create and edit rulesets.

    * [`rule_template_with_examples.yml`](/_templates/rule_template_with_examples.yml): A template for the YAML rulesets included in `/data/stylerules/`. This file is heavily annotated to provide an in-depth explanation of how YAML rulesets work.

* [`/assets/`](/assets/): A folder for storing miscellaneous site assets.

    * [`/images/`](/assets/images/): A folder for storing image files.

    * [`/js/zzzz-search-data.json`](/assets/js/zzzz-search-data.json): Just the Docs uses this file to create [search index data](https://just-the-docs.github.io/just-the-docs/docs/search/).

* [`/pages/`](/pages/): Jekyll's [Pages subdirectory](https://jekyllrb.com/docs/pages/).

    * [`/all/`](/pages/all/): This folder contains [hidden pages](https://alexakreizinger.github.io/styleguidetemplate/all/) that display all style rules in your ruleset files. These pages aren't accessible from the demo site's navigation bar, but you can see them if you manually visit their respective URLs. 

    * [`/dev/`](/pages/dev/): This folder contains the [Developers](https://alexakreizinger.github.io/styleguidetemplate/dev/) landing page and subpages that display developer-specific style rules. For more information, see [Audiences](#audiences) and [Create and edit pages](#create-and-edit-pages).

    * [`/mktg/`](/pages/mktg/): This folder contains the [Marketers](https://alexakreizinger.github.io/styleguidetemplate/mktg/) landing page and subpages that display marketer-specific style rules. For more information, see [Audiences](#audiences) and [Create and edit pages](#create-and-edit-pages).

    * [`/tw/`](/pages/tw/): This folder contains the [Technical Writers](https://alexakreizinger.github.io/styleguidetemplate/tw/) landing page and subpages that display technical writer-specific style rules. For more information, see [Audiences](#audiences) and [Create and edit pages](#create-and-edit-pages).

    * [`general_principles.md`](/pages/general_principles.md): The [General Principles](https://alexakreizinger.github.io/styleguidetemplate/general/) page, which includes basic style principles that apply to all audiences. This is an audience-agnostic page; it does not use single-sourced data.
    
    * [`style_checklist.md`](/pages/style_checklist.md): The [Style Checklist](https://alexakreizinger.github.io/styleguidetemplate/checklist/) page, which includes a collection of "minimum viable docs" style guidelines for all audiences. This is an a audience-agnostic page; it does not use single-sourced data.

* [`.gitignore`](/.gitignore): A standard gitignore file. You can edit or delete this file to suit your own needs.

* [`Gemfile`](/Gemfile): A standard [Gemfile](https://jekyllrb.com/docs/ruby-101/#gemfile). Don't modify this file unless you need to add a new Gem to your style guide site.

* [`LICENSE.md`](/LICENSE.md): A copy of the GNU GPL-3 license, under which this template is distributed.

* [`README.md`](/README.md): This readme file. ;)

* [`_config.yml`](/_config.yml): The [Jekyll configuration file](https://jekyllrb.com/docs/configuration/) for the demo site. You'll need to edit this file when you [set up the scaffolding](#quickstart) for your style guide site; you can also add or modify a variety of config values to take advantage of [site customization](#theming-and-site-customization) options.

* [`index.md`](/index.md): The [homepage](https://alexakreizinger.github.io/styleguidetemplate/). This is an audience-agnostic page; it does not use single-sourced data.

* [`robots.txt`](/robots.txt): The robots.txt file for the template's demo site. You can edit or delete this file to suit your own needs.

</details>

([return to table of contents](#table-of-contents))

## Theming and site customization
This template's demo site uses the [Just the Docs](https://github.com/just-the-docs/just-the-docs) Jekyll theme. I recommend referring to their documentation for more information about [configuring](https://just-the-docs.github.io/just-the-docs/docs/configuration/) your site via built-in theme features, [customizing](https://just-the-docs.github.io/just-the-docs/docs/customization/) your site theme further via .scss files, and a variety of additional [UI components](https://just-the-docs.github.io/just-the-docs/docs/ui-components) that the theme offers (like buttons and callouts).

You're also welcome to modify your own style guide site to use the Jekyll theme of your choosing—however, since this template was built with Just the Docs in mind, changing the theme may require you to override and/or modify a bunch of stuff that I hadn't anticipated. In other words, rework themes at your own risk!

([return to table of contents](#table-of-contents))

## License
AK's Style Guide Template is distributed under the GNU General Public License. For more information, see [`LICENSE.md`](/LICENSE.md).

([return to table of contents](#table-of-contents))

## Contact
This template was created by [Alexa Kreizinger](https://alexakreizinger.com/). If you have any questions, concerns, or general feedback about this template, feel free to reach out to me at alexakreizinger@gmail.com. 

([return to table of contents](#table-of-contents))