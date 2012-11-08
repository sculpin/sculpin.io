---
layout: default
title: Documentation

---

# Documentation

To see Sculpin in action we are going to generate a copy of [getsculpin.com][0]
locally.

First, clone the repository for the website:

    git clone https://github.com/sculpin/getsculpin.com.git
    cd getsculpin.com

Second, get Composer and install the project dependencies (including Sculpin):

    wget http://getcomposer.org/composer.phar
    php composer.phar install

Third, create a development configuration file (`app/config/sculpin_site_dev.yml`)
so that the generated URLs will make sense for your environment. By default,
the development build will be placed into `output_dev` so make sure to include
that in your URL.

Example:

    imports:
        - sculpin_site.yml
    url: http://my.local/websites/getsculpin.com/output_dev

Lastly, generate the site:

    php vendor/bin/sculpin generate

For additional notes make sure to check out the [README][1].

[0]: http://getsculpin.com
[1]: https://github.com/sculpin/sculpin/blob/master/README.md
