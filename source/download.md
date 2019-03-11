---
layout: default
title: Download
nav_name: download

---

# Download

There are a few of ways to download Sculpin. The easiest way is to add Sculpin
and any of its development dependencies to the `composer.json` for your site.

> Don't have a `composer.json` yet? No worries - running the `composer
> require` command can automatically create one for you. Or, you can run
> `composer init` to create a blank starting point.

Confused about which option is best for your use case? Ask the
Sculpin [community]({{site.url}}/community/)! They will be happy to help. :)

<br>

## Install with Composer

Sculpin can be added to any existing Composer managed project by requiring
it:

    composer require sculpin/sculpin

The entry point for sculpin is now `vendor/bin/sculpin`.

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

Note:

Originally, we recommended to install Sculpin globally. This has been
deprecated, because each Sculpin site can have specific runtime dependencies.
