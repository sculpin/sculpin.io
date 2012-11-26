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

Third, generate the site:

    vendor/bin/sculpin generate

Fourth, there is no step four! Find your freshly generated static site in `output_dev/`!

## Slightly More Advanced Options

### Overriding URL While Generating Site

Unless you have your webserver setup to serve files directly from `output_dev/`,
you will probably want to specify a custom base URL. This will ensure that
anything that references {{ site.url }} (like CSS and javascript assets) will
be found properly.

    sculpin generate --url=http://my.local/websites/getsculpin.com/output_dev

### Environments

Sculpin is aware of environments. Most examples will focus on **prod** (production)
and **dev** (development).

    sculpin generate --env=prod

Files will output to `output_${env}/` by default.

Configuration files will first be read from `app/config/sculpin_site_${env}.yml`.
If a site configuration does not exist for the specified environment, the base
configuration at `app/config/sculpin_site.yml` will be read.

### Environment Specific Configuration Example

To ensure that the URL is always appropriate for your development environment, you
can create a custom site configuration file for the development environment.

Example:

    imports:
        - sculpin_site.yml
    url: http://my.local/websites/getsculpin.com/output_dev

### Deployment

Deployment is not baked into Sculpin yet. A simple script like this is currently
being used to deploy getsculpin.com:

    sculpin generate --env=prod
    sculpin assets:install --env=prod output_prod
    rsync -avze 'ssh -p 999' output_prod/ user@yoursculpin.com:public_html

By default, `--env=prod` will cause Sculpin to place the build in `output_prod/`
and will try to load configuration from `app/config/sculpin_site_prod.yml`.


## Questions?

Check out the Sculpin [community]({{site.url}}/community) if you have questions.

[0]: http://getsculpin.com
[1]: https://github.com/sculpin/getsculpin.com
