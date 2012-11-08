---
layout: default
title: Documentation

---

# Documentation

## Live Example &mdash; Building getsculpin.com!

To see Sculpin in action we are going to generate a copy of [getsculpin.com][0]
locally. You can browse the source for the site [on GitHub][1].

First, clone the repository for the website:

    git clone https://github.com/sculpin/getsculpin.com.git
    cd getsculpin.com

Second, get Composer and install the project dependencies (including Sculpin):

    wget http://getcomposer.org/composer.phar
    php composer.phar install

Third, create a development configuration file (`app/config/sculpin_site_dev.yml`)
so that the generated URLs will make sense for your environment. By default,
the development build will be placed into `output_dev/` so make sure to include
that in your URL.

Example:

    imports:
        - sculpin_site.yml
    url: http://my.local/websites/getsculpin.com/output_dev

Lastly, generate the site:

    php vendor/bin/sculpin generate

The previous command should be run any time files have changed, whether they be
content, templates, or assets.

### Deployment

Deployment is not baked into Sculpin yet. A simple script like this is currently
being used to deploy getsculpin.com:

    sculpin generate --env=prod
    sculpin assets:install --env=prod output_prod
    rsync -avze 'ssh -p 999' output_prod/ user@yoursculpin.com:public_html

By default, `--env=prod` will cause Sculpin to place the build in `output_prod/`
and will try to load configuration from `app/config/sculpin_site_prod.yml`.


### Questions?

Check out the Sculpin [community]({{site.url}}/community) if you have questions.

[0]: http://getsculpin.com
[1]: https://github.com/sculpin/getsculpin.com
