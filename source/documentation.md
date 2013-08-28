---
layout: default
title: Documentation
nav_name: documentation

---

# Documentation

Until Sculpin has more formal documentation it is best to "learn by example."
First, [download Sculpin][1], then check out the [Sculpin blog skeleton][2]
(instructions in the README) to quickly fire up a basic Sculpin powered blog.

After that, check out the list of sites powered by Sculpin on the [home page][3]
for sites that have their source published. There should be a lot of great ideas
there! Have questions? Ask the Sculpin [community!][4]


## Sculpin and Embedded Composer

### What is Embedded Composer?

Sculpin embeds Composer into itself to reduce the requirement to download and
install Composer prior to using Sculpin. Additionally, since Sculpin is shipped
as a phar, embedding Composer allows Sculpin to remain extensible at runtime.

This should hopefully remain largely transparent to users with two exceptions.
First, it introduces two files to keep track of, `sculpin.json` and
`sculpin.lock`. Second, there are a handful of required dependencies that are
needed to be required in `sculpin.json`.


### What are sculpin.json and sculpin.lock?

Unless you are downloading Sculpin via Composer (by requiring Sculpin in a
`composer.json` file) Sculpin will look for `sculpin.json` for any install
or update commands. There is nothing fancy about `sculpin.json` as it is simply
a `composer.json` with a different name.

Along those same lines, `sculpin.lock` is just a `composer.lock` with a
different name.

This is to ensure that you will never unintentionally mix and match Composer
installed Sculpin (considered advanced functionality) with globally installed
versions of Composer (phar or shared development versions of Sculpin). Doing so
may result in [lockfile thrashing][5].

If there is a `sculpin.json`, you should run `sculpin install`. If there is a
`composer.json`, you should run `composer install`.

Sculpin will run *without* a `sculpin.json`. It is only needed if you need to
add additional dependencies specific to your site or project.


### Which dependencies are required in sculpin.json?

Unfortunately, Composer is still a ways off from a stable release. The end
result is that anything that depends upon Composer must require `dev` stability
for `composer/composer`.

Sculpin also depends on Embedded Composer. Since this project depends on
Composer itself, it won't be stable for quite some time either.

If you need to create a `sculpin.json`, the bare minimum you'll need in order to
successfully run `sculpin install` will be the following:

    {
        "require": {
            "sculpin/sculpin": "2.*@dev",

            "dflydev/embedded-composer-console": "@dev",
            "dflydev/embedded-composer-core": "@dev",
            "composer/composer": "@dev"
        }
    }

If you add additional dependencies to `sculpin.json`, they will be evaluated
against the dependencies shipped with Sculpin itself. Anything new will be
downloaded and installed into `.sculpin/` (which is exactly like a typical
Composer `vendor/` directory).



[1]: {{site.url}}/download/
[2]: https://github.com/sculpin/sculpin-blog-skeleton
[3]: {{site.url}}/
[4]: {{site.url}}/community/
[5]: https://speakerdeck.com/simensen/embedded-composer-sflive-portland-2013?slide=71
