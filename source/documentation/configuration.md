---
title: Configuration
slug: configuration

---

For Sculpin configuration there are a few things to keep in mind. First,
configuration can be environment specific. After that, there are two main ways
to configure Sculpin: site meta data and kernel configuration.

---

## Development and Production Environments

Sculpin can be run in two modes, dev and production. These are known as
environments. By default Sculpin will generate your site for the `dev`
environment. This is important to know because configuration can be based on
environment.

In order to generate your site for a production environment (`prod`), you need to
specify this in your command line:

    sculpin generate --watch --server --env=prod


---

## Site Meta Data

The easiest way to "configure" Sculpin is to add site meta data. Site meta data
can be added to any of the following files:

    |-- app/
    |  `-- config/
    |     |-- sculpin_site.yml         # Site meta data (optional)
    |     `-- sculpin_site_${env}.yml  # Environment specific meta data (optional)


### Environment Aware Configuration

Environment specific meta data overrides generic meta data so sane defaults can
be added to `sculpin_site.yml` and overridden on an environment-by-environment
basis. This can be useful for things like Google Analytics identifiers. Set the
default development version in `sculpin_site.yml` and set the production value
in `sculpin_site_prod.yml`.

Merging the `sculpin_site.yml` is not automatic. It must be imported into an
environment specific configuration file like this:

    imports:
        - sculpin_site.yml
    google_analytics_tracking_id: UA-PRODUCTION-372

---

## Sculpin Kernel Configuration

Some parts of Sculpin, specifically anything configured as a bundle, must be
configured at the kernel level. This can be done by modifying the
`sculpin_kernel.yml` file.

    |-- app/
    |  `-- config/
    |     `-- sculpin_kernel.yml       # Sculpin's configuration (optional)


For example, to configure something like the default permalink for all sources,
one would need to configure the Sculpin bundle's configuration:

    sculpin:
        permalink: pretty

Or if one need to ignore all the files ending with ~, one could:

    sculpin:
        ignore: ["**/*~"]

Or if one wanted to change the theme, one would:

    sculpin_theme:
        theme: acme/awesome-theme

It is up to a bundle to define whether or not it can be configured using site
meta data or kernel configuration. In general, kernel configuration is probably
where configuration will happen for things that are not source (read, runtime
based on stuff in `source/`) dependent.

## Permalinks

Sculpin supports multiple styles of permalinks.

- `none`: The pathname of your source file. For example: `source/about.html` would result in `about.html` and `source/_projects/sculpin.html` would result in `_projects/sculpin.html`
- `date`: Replaces dashes with slashes to have a permalink popular in many blogs. For example: `source/2014-04-10-article.html` would result in `2014/04/10/article.html`
- `pretty`: This style adds `index.html` to the name of the source file, allowing you to have permalinks without the `.html` file extension. For example: `source/about.html` would result in `about/index.html`. It also supports files with dates, for example, `source/2014-04-10-article.html` would result in `2014/04/10/article/index.html`.

Additionally you can create custom permalinks using the following tags:

- `:year`: A full numeric representation of a year, 4 digits
- `:yr`: A two digit representation of a year
- `:month`: Numeric representation of a month, with leading zeros
- `:mo`: Numeric representation of a month, without leading zeros
- `:day`: Day of the month, 2 digits with leading zeros
- `:dy`: Day of the month without leading zeros
- `:title`: Slugified title of the page
- `:slug_title`: Slug or slugified title of the page if no slug exists
- `:filename`: Filename of the page, for example, `about.html`
- `:slug_filename`: Slug or filename if no slug exists
- `:basename`: Basename of the page, for example, `source/_projects/sculpin.html` would result in `sculpin`
- `:basename_real`: Basename of the page including the extension, for example, `source/_projects/sculpin.html` would result in `sculpin.html`

A custom permalink configuration could look like this:

    sculpin:
        permalink: blog/:year/:month/:day/:slug_title
