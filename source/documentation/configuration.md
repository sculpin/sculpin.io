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
enviornments. By default Sculpin will generate your site for the dev
environment. This is important to know because configuration can be based on
environment.

In order to generate your site for a production environment (prod), you need to
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

Or if one wanted to change the theme, one would:

    sculpin_theme:
        theme: acme/awesome-theme

It is up to a bundle to define whether or not it can be configured using site
meta data or kernel configuration. In general, kernel configuration is probably
where configuration will happen for things that are not source (read, runtime
based on stuff in `source/`) dependent.
