---
layout: default
title: Download
nav_name: download

---

# Download

The easiest way to download Sculpin is to head over to the
[Get Started](/getstarted/) guide. The guide walks you through creating
a Sculpin-based blog.

Another option is to add Sculpin to the `composer.json` for your site.
This is particularly useful if the site you're planning to create is not
specifically a blog.

> Don't have a `composer.json` yet? No worries - running the `composer
> require` command can automatically create one for you. Or, you can run
> `composer init` to create a blank starting point.

Confused about which option is best for your use case? Ask the
Sculpin [community]({{site.url}}/community/)! They will be happy to help. :)

---

## Install with Composer

Sculpin can be added to any existing Composer managed project by requiring
it:

    composer require sculpin/sculpin

The entry point for running Sculpin commands is `vendor/bin/sculpin`.

> The best version of Sculpin to be running right now is version 3.0.

---

## Download via Git

Sculpin can be downloaded with git. This is mainly useful if you want to work
on changes to sculpin. Either clone the Sculpin project directly or fork and
clone the fork:

    git clone git@github.com:sculpin/sculpin.git
    cd sculpin
    composer install

At this point, `bin/sculpin` should be usable.

**Note:**

In the past, it was recommended to install Sculpin globally. This has
been deprecated for various reasons, including moving away from the
"phar" approach to Sculpin distribution.

Installing Sculpin on a per-site basis using Composer allows greater
flexibility with dependencies.
