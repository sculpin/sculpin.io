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

Sculpin is a PHP static site generator. If you like and are familiar with PHP, Sculpin
should be a natural fit.

Sculpin and all of its dependencies are managed by [Composer](http://getcomposer.org).
This may not seem like a big deal, but this means that installing Sculpin, its dependencies,
and any dependencies specific to a project can be handled quite easily.

Sculpin leverages the [Twig](http://twig.sensiolabs.org/) template engine to its fullest.
If you like Twig and want to use it as you would expect Twig to work (including template
inheritance) Sculpin is the right choice!

At its core is [Symfony's](http://symfony.com) [HTTP Kernel](https://github.com/symfony/HttpKernel).
This means that a bundle written for Symfony 2 could theoretically work "out of the box" with
Sculpin. While this *usually* isn't the case in practice, one useful bundle that is know to work is the
[GitHub Gist Twig Bundle](https://packagist.org/packages/dflydev/github-gist-twig-bundle).
If you are familiar with Symfony, you should feel right at home with Sculpin.


## Project Status

Sculpin continues to be **unstable**, under heavy development, and lacking in-depth documentation.
Be prepared for possible changes in core functionality requiring you to fix your existing
site.

But the Sculpin [community]({{site.url}}/community) can help!

The site you are reading is generated using Sculpin.
[View the source on GitHub!](https://github.com/sculpin/getsculpin.com) You are
encouraged to use it as an example of the most up to date feature implementations.

Head over to the [documentation]({{site.url}}/documentation) to see Sculpin in action.