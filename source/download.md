---
layout: default
title: Download
nav_name: download

---

# Download

<br>

## Download the Phar

Downloading `sculpin.phar` is the best way to get up and running with Sculpin.
It is a self-contained archive containing all of its dependencies and is ready
to run. You can download it like this:

    curl -sS -O https://download.sculpin.io/sculpin.phar

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

<br>

## Download via Composer

Sculpin can be added to any existing Composer managed project by simply
requiring Sculpin in `composer.json`.

    {
        "sculpin/sculpin": "2.*@dev"
    }

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
