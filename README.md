# Style Guide Template
This style guide template uses YAML files to single-source style rules accross multiple audiences.

## Repo basics

All of the following information relates to the `main` branch. For all intents and purposes, ignore (but do not delete) the `gh-pages` branch. (For more information, consult the `.github/workflows/build-jekyll.yml` section below.)

### `_data/stylerules`

The actual style rules are hosted here (in the form of YAML files). If the Liquify plugin is enabled, you can include Liquid tags in the actual data files and "liquify" them later. (For more information, consult the "How to use Liquify" section below.)

### `_includes`

The Liquid loops that pull style rules from their data files. Designed to be modular so you can include the file in your output page rather than re-typing the Liquid all over again.

#### `get_all_rules.md`
Outputs every single rule in a given `_data/stylerules/` file. Currently used for the semi-secret `/all/` pages.
    
**Usage** (when including in an actual page):
``` 
{% assign file = site.data.stylerules.[YOURFILE] %}

{% include get_all_rules.md filename=file %}
```

#### `get_rules_for_audience`
Outputs every applicable rule in a given `_data/stylerules/` file based on your audience of choice (current options: `dev`, `mktg`, and `tw`). 

> **NOTE** : Does not accept `all` as an audience. If you want to output all style rules, use `get_all_rules.md` instead.

**Usage** (when including in an actual page):
```
{% assign file = site.data.stylerules.[YOURFILE] %}
{% assign aud = "[YOURAUDIENCE]" %}

{% include get_rules_for_audience.md filename=file audience=aud %}
```             
#### `get_featured_rules_for_audience`
Outputs every "featured" rule in a given `_data/stylerules/` file based on your audience of choice (current options: `dev`, `mktg`, and `tw`). Currently used on parent pages for each audience.

**Usage** (when including in an index page):
```
{% assign aud = "[YOURAUDIENCE]" %}
{% assign file1 = site.data.stylerules.[YOURFILE] %}
{% assign section1 = "[SECTIONNAME]" %}
{% capture link1 %}{{site.baseurl}}{{page.permalink}}[URL-OF-PAGE-WHERE-THESE-RULES-APPEAR/]{% endcapture %}

{% include get_featured_rules_for_audience.md filename=file1 audience=aud sectionname=section1 sectionlink=link1 %}
```
> **NOTE** : You'll need to repeat `file1`/`section1`/`link1` (and its associated `include` statement) as many times as needed to fetch the features rules from every section. However, `aud` should be consistent, so there's no need to repeat that part.

### `_plugins/liquify.rb`

Sourced from [here](https://github.com/vividh/liquify). For more information about using Liquify, consult the "How to use Liquify" section below. 

### `_github/workflows/build-jekyll.yml`

A custom GitHub Actions workflow that lets you deploy the GitHub Pages site as if you were running Jekyll locally. Crucial if I want to use non-approved plugins like Liquify. Some details:

* The GitHub Pages branch must be set to `gh-pages` rather than `main`. 

* Every time you push a change to `main`, the `build-jekyll` workflow will automatically crate the "actual" site files and push them to `gh-pages`.

* GitHub's default GitHub Action will then automatically generate the GitHub pages site from the `gh-pages` repo.

In other words, stick to making changes in `main` as usual and don't touch anything in `gh-pages`. 

### `pages`

The `pages` folder for the actual style guide output. Each audience has its own subfolder (`pages/dev`, `pages/mktg`, and `pages/tw`), and each subfolder contains the pages associated with that audience.

> **NOTE:** The `^[AUDIENCE].index.md` files start with a caret so that the index file will appear first alphabetically (because it's convenient when it's at the top of the list). The caret doesn't serve an actual purpose, Jekyll-wise.

* For example, `pages/mktg/grammar.md` generates a page you can visit at https:/alexakreizinger.github.io/styleguidetemplate/mktg/grammar/. 

* The page itself pulls data from `_data/stylerules/grammar.yml`. It does this by using `include` to call upon the `get_rules_for_audience.md` (where the filename is `site.data.stylerules.grammar` and the audience is `mktg`).

* As such, the output will include all style rules from `_data/stylerules/grammar.yml` that are aimed at marketers.

#### **All**
* audience: `all` (see note below)
* url: `all`
* title: All
* (semi-secret; hidden from nav and search, but accessible by visiting https://alexakreizinger.github.io/styleguidetemplate/all/)
#### **Developers**
* audience: `dev`
* url: `/dev/`
* title: Developers
#### **Marketers**: 
* audience: `mktg`
* url: `/mktg/`
* title: Marketers
#### **Technical Writers**
* audience: `tw`
* url: `/tw/`
* title: Technical Writers

> **NOTE:** Some of the Liquid stuff for autogenerating links between pages is way easier when an audience's `audience` value and `url` slug are the same. As such, the `all` audience has an audience key just to make the URL part easier, even though the audience value isn't used to fetch any rules from the YAML files.

### `YAMLtemplate.yml`

Template for the YAML files in `_data/stylerules`. Not actually referenced by any other pages, this is just a regular old template to make it easier to create and wrangle style rule files with the correct syntax.

## How to use Liquify

If output from a `{{ Liquid tag }}`' includes text that *itself* contains a Liquid tag, you can use the `{{ content | liquify }}` syntax to also parse the output's own Liquid tags and populate them accordingly.

For example:

`page.md` contains the following front matter and content:

```
---
title: My Page
tagline: {{ page.title }} — Population: You
---

{{ page.tagline }}
```
Under normal circumstances, this would render the following output (the literal contents of the `page.tagline` item):

`{{ page.title }} — Population: You`

However, if you use `liquify` in `page.md`...
```
---
title: My Page
tagline: {{ page.title }} — Population: You
---

{{ page.tagline | liquify }}
```
...you'd render the following output (with the `page.tagline` item's own Liquid rendered accordingly):

`My Page - Population: You`

> **NOTE:** Tags are parsed on the final page or file they're rendered on, not the page or file in which `liquify` is initially called. That is to say, if you use `include` to call upon another page that uses the `liquify` tag, the tag will use any `page.variables` from the page where the `include` was *called*, not the location of the `include` file itself. 

### Liquify and hyperlinks
The main reason I'm using Liquify here is to create hyperlinks between different style rule pages.

For example:

`grammar.yml` includes the following content:

```
      For more information, see [APIs and SDKs]({{site.baseurl}}/{{page.audience}}/apis-and-sdks/) and [Procedural Instructions]({{site.baseurl}}/{{page.audience}}/formatting-and-organization/#procedural-instructions).
    audience: [tw, dev]
```
Since this particular content is applicable to both developers and technical writers, it's impossible to hard code these links without having to create two separate entries for both audiences—which would defeat the purpose of single-sourcing!

Instead, we want to automatically replace `{{page.audience}}` with either `dev` or `tw`, based on whichever one is appropriate at the time. So if I wanted to fetch all grammar rules for technical writers, I'd use the following syntax in the `/pages/tw/tw_grammar.md` file:

```
{% assign file = site.data.stylerules.grammar %}
{% assign aud = page.audience %}

{% include get_rules_for_audience.md filename=file audience=aud %}
```
And the included `get_rules_for_audience.md` file is where the `liquify` magic happens:

```
[...]
{% if stylerule.audience contains include.audience %}
{{ stylerule.rule | liquify }}
[...]
```

So when the text is rendered in `/pages/tw/tw_grammar.md`, `{{page.audience}}` is replaced with the relevant variable in that page's YAML front matter. In this case, the value in question is `tw`, which will turn `/{{page.audience}}/apis-and-sdks/` into `/tw/apis-and-sdks/`. And if we did the same thing for a developer audience, it'd give us the correct `dev` URL.


## Miscellaneous

* To get multiline bullet points for `rules` or `examples`, either use a <br> tag after the first line of text.
