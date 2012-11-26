---
layout: default
full_title: Sculpin &mdash; PHP Static Site Generator
fancy_index: true

---

## What is Sculpin?

Sculpin is a PHP static site generator.

Sculpin takes plain old text files (Markdown, Textile, etc.) and combines them with Twig
templates to produce a set of static HTML files that can be easily deployed to almost any
hosting platform.


## Why Sculpin?

### PHP

Sculpin is a **PHP static site generator**. If you like and are familiar with PHP, Sculpin
should be a natural fit.


### Composer

Sculpin and all of its dependencies are managed by [Composer](http:/getcomposer.com).
This may not seem like a big deal, but this means that installing Sculpin, its dependencies,
and any dependencies specific to a project, can be handled quite easily.


### Building Blocks

Sculpin is built on top of several incredible PHP projects. By relying on these projects
Sculpin did not have to reinvent too many wheels.


#### Twig — Template Engine

Sculpin leverages the [Twig](http://twig.sensiolabs.org/) template engine to its fullest.
If you like Twig and want to use it as you would expect Twig to work (including template
inheritance) Sculpin is the right choice!


#### Composer — Dependency Management

Sculpin has embedded [Composer](http://getcomposer.org/) in itself to manage
plugins. This means that not only can Sculpin be installed by Composer, new
functionality can be added to sites easily using the site's `composer.json`.


#### Symfony Components

Sculpin is written using a selection of Symfony Components.

At its core is [HTTP Kernel](https://github.com/symfony/HttpKernel). This means that
a bundle written for Symfony 2 could theoretically work "out of the box" with Sculpin.
While this *usually* isn't the case in practice, one useful bundle that is know to work is the
[GitHub Gist Twig Bundle](https://packagist.org/packages/dflydev/github-gist-twig-bundle).


### Why Sculpin Instead of  Jekyll, Octopress, or Phrozn?

There are many static site generators out there. These three stand out due to a
combination of their popularity and maturity (Jekyll and Octopress) or their similarity
(Phrozn is a Twig based PHP static site generator).

[Jekyll](https://github.com/mojombo/jekyll) is wildly popular since it backs
[GitHub Pages](http://pages.github.com/). [Octopress](http://octopress.org/), based on
Jekyll, is pretty popular in the tech scene on account of its built-in set of plugins
and its pretty and responsive hacker-friendly default theme.

[Phrozn](http://www.phrozn.info/) is another PHP static site generator that is similar
to Sculpin on the surface. It supports several text file formats and uses Twig templates.

Sculpin sets itself apart from these three by fully leveraging Twig. Jekyll (and by
extension Octopress) with Liquid and Phrozn with Twig render the content seperate from
the containing template. This severely limits the ability to use the full power of
the underlying template language by not leveraging template inheritance.

Sculpin, on the other hand, treats the content as if it was a template and properly
extends the request layouts using Twig template inheritance the way it was intended.


## Project Status

Sculpin continues to be **unstable**, under heavy development, and lacking
documentation. Be prepared for possible changes in core functionality requiring
you to fix your existing site.

But the Sculpin [community]({{site.url}}/community) can help!

The site you are reading is generated using Sculpin.
[View the source on GitHub!](https://github.com/sculpin/getsculpin.com) You are
encouraged to use it as an example of the most up to date feature implementations.

Start by reading the [documentation]({{site.url}}/documentation) to see how this site is
generated.
