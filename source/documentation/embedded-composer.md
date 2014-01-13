---
title: Embedded Composer
slug: embedded-composer

---

Sculpin embeds Composer into itself to reduce the requirement to download and
install Composer prior to using Sculpin. Additionally, since Sculpin is shipped
as a phar, embedding Composer allows Sculpin to remain extensible at runtime.
This would not be possible otherwise.

This should hopefully remain largely transparent to users with two exceptions.
First, it introduces two files to keep track of, `sculpin.json` and
`sculpin.lock`. Second, there are a handful of required dependencies that are
needed to be required in `sculpin.json`.

---

## What are sculpin.json and sculpin.lock?

Unless you are downloading Sculpin via Composer (by requiring Sculpin in a
`composer.json` file) Sculpin will look for `sculpin.json` for any install
or update commands. There is nothing fancy about `sculpin.json` as it is simply
a `composer.json` with a different name.

Along those same lines, `sculpin.lock` is just a `composer.lock` with a
different name.

This is to ensure that you will never unintentionally mix and match Composer
installed Sculpin (considered advanced functionality) with globally installed
versions of Composer (phar or shared development versions of Sculpin). Doing so
may result in [lockfile thrashing][1].

If there is a `sculpin.json`, you should run `sculpin install`. If there is a
`composer.json`, you should run `composer install`.

Sculpin will run *without* a `sculpin.json`. It is only needed if you need to
add additional dependencies specific to your site or project.

[1]: https://speakerdeck.com/simensen/embedded-composer-sflive-portland-2013?slide=71
