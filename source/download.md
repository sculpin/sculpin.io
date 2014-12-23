---
layout: default
title: Download
nav_name: download

---

# Download

There are a number of ways to download Sculpin. The easiest way is to download
the phar. Most of the examples will assume this is how Sculpin has been
installed. Depending on what you want to do, your level of experience with
Sculpin, and your level of experience with Composer, one of the other options
*may* be more appropriate.

Confused about which option is best for your use case? Ask the
Sculpin [community]({{site.url}}/community/)! They will be happy to help. :)

<br>

## Download the Phar

Downloading `sculpin.phar` is the best way to get up and running with Sculpin
since it is a ready to run self-contained archive. You can download it like
this:

    curl -O https://download.sculpin.io/sculpin.phar

You can execute Sculpin by running `php sculpin.phar` but if you want to skip
the `php` part, you can make `sculpin.phar` executable like this:

    chmod +x sculpin.phar

To make things even easier, `sculpin.phar` can be renamed to `sculpin` like
this:

    mv sculpin.phar sculpin

Finally, if you move `sculpin` to your path it can be run from anywhere. For
example, assuming `~/bin` is in your `$PATH`, you can do the following:

    mv sculpin ~/bin/

That's it! You're all set to run Sculpin. :)

You can also download stable releases of Sculpin at the following URLs:

 * [https://download.sculpin.io/release/v2.0.0/sculpin.phar](https://download.sculpin.io/release/v2.0.0/sculpin.phar)

<br>

## Download via Composer

Sculpin can be added to any existing Composer managed project by simply
requiring Sculpin (and a couple of other dev dependencies) in `composer.json`.

    {
        "require": {
            "sculpin/sculpin": "~2.0",
    
            "dflydev/embedded-composer-console": "@dev",
            "dflydev/embedded-composer-core": "@dev",
            "composer/composer": "@dev"
        }
    }

Sculpin currently relies on Embedded Composer and Composer, neither of which
have a stable release. In order to avoid having to set `minimum-stability` to
dev, these packages can be flagged as `@dev` to ensure Composer will install
everything correctly.

By default this will install Sculpin to `vendor/bin/sculpin`.


### Important Notice Regarding Composer

Installation via Composer is considered advanced functionality. Running a
globally installed version of Sculpin against a project that has Sculpin
included via Composer can have unexpected results. Never mix and match!

<br>

## Download via Git

Sculpin can be downloaded via git to be used while being under development.
Either clone the Sculpin project directly or fork and clone the fork.

    git clone git@github.com:sculpin/sculpin.git
    cd sculpin
    composer install

At this point, `bin/sculpin` should be useable.

If you want to make your development version of Sculpin available, create a
symlink to it from somewhere in your `$PATH`. For example, to create a
`sculpin-dev` command and assuming that `~/bin` is in your `$PATH`, execute the
following:

    ln -s ~/sculpin/bin/sculpin ~/bin/sculpin-dev

This will allow you to have a globally installed version of Sculpin (like maybe
`sculpin.phar`) along side a development version of Sculpin (`sculpin-dev`).

### Important Notice Regarding Git

Installation via git is considered advanced functionality. This method of
downloading Sculpin is only recommended for people who intend to work directly
on Sculpin itself.
