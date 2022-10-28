# Dananke, a theme for [Hugo](https://gohugo.io/)

## Status

[![build-and-verify](https://github.com/danielfdickinson/dananke-theme-hugo-dfd/actions/workflows/build-and-verify.yml/badge.svg)](https://github.com/danielfdickinson/dananke-theme-hugo-dfd/actions/workflows/build-and-verify.yml)

Documentation is incomplete and not in sync with current state of theme.

## ARCHIVED

This module is no longer maintained (archived for historical purposes), and will not receive updates, even security updates.

## Overview

The intent of this theme is to provide a fairly complete framework for Daniel F. Dickinson's Hugo sites with important features, and including best practices for performance and accessibility.

It is derived from the [Ananke Hugo theme](https://github.com/theNewDynamic/gohugo-theme-ananke) with many thanks to Bud Parr, Regis Philbert, and all contributors.

It has removed the use of Tachyons.

## Demo site

<https://dananke-theme.wildtechgarden.ca>

## Features

- Responsive
- Accessible
- Contact form
- Custom Robots.txt (changes values based on environment)
- RSS Discovery
- Table of Contents (must declare `toc: true` in post parameter)

### Derived from modules

Many additional features are available through modules imported into the theme.

Currently imported modules include:

- [Image handling module by DFD](https://github.com/danielfdickinson/image-handling-mod-hugo-dfd)
- [Metadata/page microformats module by DFD](https://github.com/danielfdickinson/metadata-mod-hugo-dfd)
- [Link handling module by DFD](https://github.com/danielfdickinson/link-handling-mod-hugo-dfd)

## Installation

### As a Hugo module (recommended)

> If you installed a [Hugo binary](https://gohugo.io/getting-started/installing/#binary-cross-platform), you may not have Go installed on your machine. To check if Go is installed:

```sh
go version
```

> Go modules were considered production ready in v1.14. [Download Go](https://go.dev/dl/).

1. From your project's root directory, initiate the hugo module system if you haven't already:

   ```sh
   hugo mod init github.com/<your_user>/<your_project>
   ```

2. Add the theme's repo to your `config.toml`:

   ```toml
   theme = ["github.com/danielfdickinson/dananke-theme-hugo-dfd"]
   ```

### As git submodule

Inside the folder of your Hugo site run:

```sh
git submodule add https://github.com/danielfdickinson/dananke-theme-hugo-dfd.git themes/ananke
```

For more information read the official [setup guide](https://gohugo.io/getting-started/installing/) of Hugo.

## Getting started

After installing the theme successfully it requires a just a few more steps to get your site running.

### The config file

Take a look inside the [`exampleSite`](https://github.com/danielfdickinson/dananke-theme-hugo-dfd/tree/master/exampleSite) folder of this theme. You'll find a file called [`config.toml`](https://github.com/danielfdickinson/dananke-theme-hugo-dfd/blob/master/exampleSite/config.toml). To use it, copy the [`config.toml`](https://github.com/danielfdickinson/dananke-theme-hugo-dfd/blob/master/exampleSite/config.toml) in the root folder of your Hugo site. Feel free to change the strings in this theme.

### Change the hero background

For any page or post you can add a featured image by including the local path in front matter (see content in the `exampleSite/content/_readme.md` file for examples): `featured_image: '/images/gohugo-default-sample-hero-image.jpg'`

#### Featured image as page resources

If user is using [Page Resources](https://gohugo.io/content-management/page-resources/), the theme will try and match the `featured_image` from with a page resource of type `image` and use its relative permalink. If no `featured_image` is set, the theme will look for a Page Resource of type `image` whose filepath incudes either `cover` or `feature`

#### Other hero settings

If you would like to hide the header text on the featured image on a page, set `omit_header_text` to `true`. See `exampleSite/content/contact.md` for an example.

You don't need an image though. The default background color is black, but you can change the color, by changing the default color class in the config.toml file.

### Activate the contact form

This theme includes a shortcode for a contact form that you can add to any page (there is an example on the contact page in the exampleSite folder). One option is to use [formspree.io](https://formspree.io/) as proxy to send the actual email. Each month, visitors can send you up to one thousand emails without incurring extra charges. Visit the Formspree site to get the "action" link and add it to your shortcode like this:

```html
{{</* form-contact action="https://formspree.io/x/dfdasdfa" */>}}
```

### Social follow + share

The theme automatically adds "Follow" link icons to the header and footer and "Share" link icons to pages unless `shareDisable` parameter is set to true either on the site level (site params) or page level (front matter). Each built-in service sports a label, an icon and a color.

In order to register a service to be used, user must add an `danankeSocials` parameter to its project configuration file and list them through it in the desired order. Each entry must bear a

- `name`: It matches the built-in service reference (Ex: twitter, github)
- `url`: The url of the handle's profile on the service (Ex: <https://twitter.com/theNewDynamic>, <https://github.com/theNewDynamic>)

```yaml
params:
  dananke_socials:
  - name: twitter
    url: https://twitter.com/theNewDynamic
  - name: github
    url: https://github.com/theNewDynamic
```

If user needs to overwrite default `color` and `label` of the service, they simply need to append the following to the entry:

- label: The displayed name of the service to be used to popuplate `[title]` attributes and read-only. (Ex: Twitter, GitHub)
- color: Used for styling purposes. (Ex: '#1da1f2', '#6cc644')

```yaml
params:
  dananke_socials:
  - name: twitter
    url: https://twitter.com/theNewDynamic
    label: TND Twitter
  - name: github
    url: https://github.com/theNewDynamic
    label: TND GitHub Account
    color: '#ff6800'
```

#### Limit follow or share

If a user needs to control Share and Follow of a service, for example enabling "Share on Facebook" without having a Facebook Page to "follow", they can set `follow: false` one the registered service.

```yaml
params:
  ananke_socials:
  - name: facebook
    label: Facebook
    follow: false
  - name: twitter
    url: https://twitter.com/theNewDynamic
    label: TND Twitter
```

#### Social icons customization

On top of easily customizing the built-in services' label and color, user can overwrite their icon by adding an svg file at `/assets/dananke/socials` with a filename matching the service's name.
For example, in order to use your own GitHub icon, simply add an svg file at `/assets/dananke/socials/github.svg`

#### Built-in services

Here is the list of built-in services. Those marked with an `*` are also part of the "Share" module.

- twitter*
- instagram
- youtube
- github
- gitlab
- keybase
- linkedin*
- medium
- mastodon
- slack
- stackoverflow
- facebook*
- rss

#### Complement

In order to add an unknown service (absent from the list above), you simply need to add all three settings to `dananke_socials`: name, url, label, color, and optionally add an icon file matching the `name` to the `assets/dananke/socials` directory. In the absence of an icon, the theme will print the service's label.

### CSS

Ananke stylesheet is built with Hugo Pipes's [Asset Bundling](https://gohugo.io/hugo-pipes/bundling/#readout) alone to maximize compatibility. The theme simply bundles its several files into one minified and fingerprinted (in production) CSS file.

#### Custom CSS

Custom CSS only works with Hugo Extended

In order to complement the default CSS with your own, you can add custom css files to the project.

- Just add a `assets/css/custom` directory to your project and add the file(s) in it.
- The css files will be added in their lexical order to final `main.css` file.

### Show reading time and word count

If you add a key of `show_reading_time` true to either the Config Params, a page or section's front matter, articles will show the reading time and word count.

### Adding scripts to the page head

Some scripts need to be added within the page head. To add your own scripts to the page head, simply insert them into the `head-additions.html` partial located in the `layouts/partials` folder.

### Logo

You can replace the title of your site in the top left corner of each page with your own logo. To do that put your own logo into the `static` directory of your website, and add the `site_logo` parameter to the site params in your config file. For example:

```toml
[params]
  site_logo = "img/logo.svg"
```

### Set content font color

You can set the font color of the main content both globally and on individual pages:

Globally:
Set the `text_color` param in the `config.toml` file.

```toml
[params]
  text_color = "green"
```

Individual Page (prioritized over global):
Set the `text_color` param in a page's markdown file front matter.

note: The value of `text_color` must be a valid CSS color class.

### Localize date format

Dates of blog posts and single pages are rendered with the default date format commonly used in the USA and Canada. It is possible to specify a different format.

```toml
[params]
  date_format = "2. January 2006"
```

See hugo's documentation of the [`dateFormat` function](https://gohugo.io/functions/dateformat/) for more details.

### Point to a custom sitemap on the 404 page

By default the 404 page will include text and a link to ``/about/user-sitemap``, if present. You can specify a different page using the ``sitemap404`` param (site-level only; not per-page).

```toml
[params]
sitemap404 = "asitemap"
```

### Nearly finished

In order to see your site in action, run Hugo's built-in local server.

```sh
hugo server
```

Now enter `http://localhost:1313/` in the address bar of your browser.

## Production

To run in production (e.g. to have Google Analytics show up, if used), run `HUGO_ENV=production` before your build command. For example:

```sh
HUGO_ENV=production hugo
```

Note: The above command will not work on Windows. If you are running a Windows OS, use the command below:

```cmd
set HUGO_ENV=production
hugo
```

## Contributing

If you find a bug feel free to use the [issue tracker](https://github.com/danielfdickinson/dananke-theme-hugo-dfd/issues) to let me know.

For questions, ideas, and feature suggestions please use the [discussions](https://github.com/danielfdickinson/dananke-theme-hugo-dfd/discussions).
