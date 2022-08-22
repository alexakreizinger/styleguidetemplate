<a name="readme-top"></a>
# AK's Style Guide Template

A template for building Jekyll-based style guides that use Liquid tags and YAML files to single-source style rules across multiple audiences. For an example of its output, check out the [demo site](https://alexakreizinger.github.io/styleguidetemplate/) generated from this repository. 

<details>
  <summary>Table of contents</summary>

[PUT TABLE OF CONTENTS HERE!!]

</details>

## About this template

[WRITE ABOUT SECTION]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Getting started

### Requirements
Since this template is designed to function entirely within GitHub Pages, there are technically no requirements for using it; you can make all of your changes directly within GitHub if you so choose—though this may not be advisable (or practical). However, if you'd like build a staging site locally to preview changes before committing them (which I strongly recommend), you'll need to [install Jekyll](https://jekyllrb.com/docs/installation/).

### Installation 

To build your own style guide from this template:

1. Clone this repo. (You only need to clone the `main` branch.)
2. Modify the following values in `_config.yml`:
  ```
  title: <the title of your site>
  description: <the description for your site>
  url: <the top-level domain of your site (e.g., "https://username.github.io")>
  baseurl: <the baseurl of your site (e.g., "styleguide")>
  ```
3. If you're using GitHub Pages, follow the instructions in the **Hosting with GitHub Pages** section below.

### Theme customization
This template uses the [Just the Docs](https://github.com/just-the-docs/just-the-docs) Jekyll theme, but you can modify it to use any theme of your choosing. However, the template was built with the Just the Docs theme in mind, so changing the theme may require you to override and revise a bunch of stuff that I hadn't anticipated—customize at your own risk!

### Hosting with GitHub Pages
This template also uses a custom [GitHub Actions workflow](https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions) to deploy the site to GitHub pages. Since GitHub Pages normally can't build sites that use [unsupported plugins](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll#plugins) (like the [Liquify](https://github.com/vividh/liquify) plugin, which this template can't function without), the `build-jekyll.yml` file in the `/.github/workflows/` folder is a necessary workaround. 

If you'd like to host your own style guide site with GitHub Pages, make sure not to delete this custom workflow file. Additionally, you'll need to set up your style guide repository to have two branches—`main` and `gh-pages`—and configure GitHub Pages to build from the `gh-pages` branch. The workflow then functions as follows:

* Every time you push a change to `main`, your custom action automatically uses the files in `main` to build website assets in `gh-pages`.
* GitHub Pages detects the changes in `gh-pages` and automatically generates your website from the latest assets.
* Changes are pushed to your live site.

> :warning: Don't directly edit any files in the `gh-pages` branch; when the `build-jekyll.yml` workflow runs, it overwrites the entire `gh-pages` branch. You should only make commits to `main`.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## File architecture

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## License

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version. 

For more information, see `LICENSE.md`.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contact

Alexa Kreizinger - [alexakreizinger.com](https://alexakreizinger.com/)

alexakreizinger@gmail.com

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Acknowledgements 

This template was made possible thanks to the following teams and tools:

* [Jekyll](https://jekyllrb.com/)
* [Just the Docs](https://github.com/just-the-docs/just-the-docs) Jekyll theme
* vividh's [Liquify](https://github.com/vividh/liquify) plugin
* othneildrew's [readme template](https://github.com/othneildrew/Best-README-Template) 