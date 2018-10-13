---
layout: default
title: Download
nav_name: download

---

# Download

There are a few of ways to download Sculpin. The easiest way is to add Sculpin
and any of its development dependencies to the `composer.json` for your site.
Don't have a `composer.json` yet? Create one!

Confused about which option is best for your use case? Ask the
Sculpin [community]({{site.url}}/community/)! They will be happy to help. :)

<br>

## Download via Composer

Sculpin can be added to any existing Composer managed project by simply
requiring Sculpin (and a couple of other dev dependencies) in `composer.json`.

    {
        "require": {
            "dflydev/embedded-composer": "@dev",
            "sculpin/sculpin": "^2.1"
        }
    }

By default this will install Sculpin to `vendor/bin/sculpin`.

Sculpin currently relies on Embedded Composer which does not have a stable
release. In order to avoid having to set `minimum-stability` to dev,
these packages can be flagged as `@dev` to ensure Composer will
install everything correctly.


<br>

## Download via Git

Sculpin can be downloaded via git to be used while being under development.
Either clone the Sculpin project directly or fork and clone the fork.

    git clone git@github.com:sculpin/sculpin.git
    cd sculpin
    composer install

At this point, `bin/sculpin` should be usable.

If you want to make your development version of Sculpin available, create a
symlink to it from somewhere in your `$PATH`. For example, to create a
`sculpin-dev` command and assuming that `~/bin` is in your `$PATH`, execute the
following:

    ln -s ~/sculpin/bin/sculpin ~/bin/sculpin-dev

This will allow you to have a globally installed version of Sculpin (like maybe
`sculpin.phar`) along side a development version of Sculpin (`sculpin-dev`).

### Important Notice Regarding Git

Global installation is not recommended as each Sculpin site could have runtime
dependencies that are not compatible with the globally installed version of
Sculpin. This has been a popular method of maintaining Sculpin sites in
the past, though, so notes are still left here. Just keep in mind that
it will probably be better to run the Sculpin that gets installed
specifically for your site.
