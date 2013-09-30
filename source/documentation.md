---
layout: default
title: Documentation
nav_name: documentation

---

# Documentation

Until Sculpin has more documentation it may be best to "learn by example." If
you are interested in going that route, first [download Sculpin][1] and then
check out the [Sculpin blog skeleton][2] (instructions in the README). The end
result will be a simple Sculpin blog you can start playing with.

After that, check out the list of sites powered by Sculpin on the [home page][3]
for sites that have their source published. There should be a lot of great ideas
there!

And as always, if you have questions please get in touch with the Sculpin
[community][4]! We will try to get you answers quickly. :)

## Bundles

Sculpin can be extended by building Symfony Bundles that have Sculpin's
lifecycle and events in mind. In fact, the heart of Scupin is a Symfony Bundle
called SculpinBundle. It is used to wire up everything that Sculpin needs to
run.

Some of the default Sculpin bundles have documentation available:

 * [SculpinPostsBundle][6] Adds blogging capabilities to Sculpin

## Basic Sculpin Project

A Sculpin project is capable of building exactly one static site. By default,
Sculpin assumes a basic filesystem structure for any Sculpin project.

    |-- app/
    |  `-- config/
    |     |-- SculpinKernel.php        # Custom Sculpin kernel (optional)
    |     |-- sculpin_kernel.yml       # Sculpin's configuration (optional)
    |     |-- sculpin_site.yml         # Site meta data (optional)
    |     `-- sculpin_site_${env}.yml  # Environment specific meta data (optional)
    |-- output_${env}/                 # Environment specific generated static files
    |-- source/
    |  |-- _posts/                     # Individual blog posts live here (optional)
    |  `-- _views/                     # Templates (optional)
    `-- sculpin.json                   # Dependencies (optional)

### Hello World Project

#### Hello World Directory Structure

    |-- source/
       `-- index.md

#### Smallest Source File

    ---
    ---

    # Hello World

#### Run

    sculpin generate --watch --serve

Visit [localhost:8000](http://localhost:8000) to see your new static site!


#### Ouput

Explore the `output_dev` directory to see what is happening behind the scenes:

    |-- output_dev/
    |  `-- index.html


## Configuration

### sculpin_site.yml and sculpin_site_${env}.yml

The easiest way to "configure" Sculpin is to add site meta data. Site meta data
can be added to any of the following files:

    |-- app/
    |  `-- config/
    |     |-- sculpin_site.yml         # Site meta data (optional)
    |     `-- sculpin_site_${env}.yml  # Environment specific meta data (optional)


Environment specific meta data overrides generic meta data so sane defaults can
be added to `sculpin_site.yml` and overridden on an environment-by-environment
basis. This can be useful for things like Google Analytics identifiers. Set the
default development version in `sculpin_site.yml` and set the production value
in `sculpin_site_prod.yml`.

Merging the `sculpin_site.yml` is not automatic. It must be imported into an
enviornment specific configuration file like this:

    imports:
    - sculpin_site.yml
    google_analytics_tracking_id: UA-PRODUCTION-372

### sculpin_kernel.yml

Some parts of Sculpin, specifically anything configured as a bundle, must be
configured at the kernel level. This can be done by modifying the
`sculpin_kernel.yml` file.

    |-- app/
    |  `-- config/
    |     `-- sculpin_kernel.yml       # Sculpin's configuration (optional)


For example, to configure something like the default permalink for posts, one
would need to configure the posts bundle's configuration:

    sculpin_posts:
        permalink: blog/:year/:month/:day/:filename/

Or if one wanted to change the default Markdown parser class, one would:

    sculpin_markdown:
        parser_class: Michelf\Markdown

It is up to a bundle to define whether or not it can be configured using site
meta data or kernel configuration. In general, kernel configuration is probably
where configuration will happen for things that are not source (read, runtime
based on stuff in `source/`) dependant.


## Sources

By default, sources are objects represented by each file under `source/`.
Sources that have YAML frontmatter are considered special in that they can be
formatted.

What is YAML frontmatter? It is best to compare examples:

    # This is a markdown file without YAML frontmatter

... compared to...

    ---
    layout: default
    ---

    # This is a markdown file with YAML frontmatter

As you can see, there is a chunk of YAML in the second example. It is delimited
by `---`. The YAML frontmatter is parsed and injected into every page rendering
and is accessible as `page.KEY`.


### Deep Frontmatter YAML Structures

Sculpin will read deep structures in YAML frontmatter. Just use a `.` to
indicate that you want to descend into a structure. For example:

    ---
    layout: default
    something:
        here:
            very: deep
            also: deep
    ---

    {% verbatim %}We can reference `{{ page.something.here.also }} === deep`.{% endverbatim %}


## Sources and Layouts

Many static site generators, including Jekyll and Phrozn, will render each
source first, and inject the resulting output into the layout. While this
approach (the "russian dolls" approach) is simpler, it means you end up losing
the inheritance capabilities thare built into both Twig and Liquid.

Sculpin attempts to solve this problem by wrapping each source in a block named
"content." So, given the following file:

    ---
    layout: default
    ---

    # This is a markdown file with YAML frontmatter

Internally, Sculpin treats this file like the following:

    {% verbatim %}{% extends "default" %}{% endverbatim %}
    {% verbatim %}{% {% endverbatim %}block content{% verbatim %} %}{% endverbatim %}

    # This is a markdown file with YAML frontmatter
    {% verbatim %}{% {% endverbatim %}endblock{% verbatim %} %}{% endverbatim %}




The end result is that each source file can be rendered together in one go
rather than rendering the content by itself and injecting the content into the
wrapper template. This means that additional data can be passed from the source
into the wrapper template!

Given a source file like this:

    ---
    layout: default
    special_value: nice
    ---

    # This is a markdown file with YAML frontmatter

One can reference the `special_value` key in the `default` template like this:

    {% verbatim %}<html>
    {% if page.special_value is defined %}
        Special value exists and is <strong>{{ page.special_value }}</strong>!.
    {% endif %}{% endverbatim %}
    {% verbatim %}{% {% endverbatim %}block content{% verbatim %} %}{% endverbatim %}Fallback content{% verbatim %}{% {% endverbatim %}endblock{% verbatim %} %} {% endverbatim %}
    </html>





After rendering, the final result will be:

    <html>
        Special value exists and is <strong>nice</strong>!.
    <h1>This is a markdown file with YAML frontmatter</h1>
    </html>


## Converters

Converters will convert incoming markup to something else, generally HTML.
Sculpin ships with two converters, Markdown and Textile.

### Markdown Converter

The Markdown Converter will convert `.md`, `.mdown`, and `.markdown` files
using [michelf/php-markdown](https://packagist.org/packages/michelf/php-markdown).

#### Configuration

The Markdown Converter can be configured by adjusting the following
`sculpin_kernel.yml` settings:

 * **sculpin_markdown.parser_class**:
   Can be one of `Michelf\MarkdownExtra` or `Michelf\Markdown`. Default value is `Michelf\MarkdownExtra`.
 * **sculpin_markdown.extensions**:
   Default value is `['.md', '.mdown', '.markdown']`.


### Textile Converter

The Textile Converter will convert `.textile` files using
[netcarver/textile](https://packagist.org/packages/netcarver/textile).

#### Configuration

The Textile Converter can be configured by adjusting the following
`sculpin_kernel.yml` settings:

 * **sculpin_textile.extensions**:
   Default value is `['.textile']`.

## Formatters

Formatters are responsible for formatting sources. This can be considered a view
or template layer.

Sculpin ships with one formatter, Twig.


### Twig Formatter

The Twig Formatter is responsible for laying out individual sources into nicer
"complete" files. Most of the time this will be formatting into an HTML file but
there are definitely cases when files will be formatted as CSS, JavaScript, or
XML (Atom or RSS).


#### Configuration

The Twig Formatter can be configured by adjusting the following
`sculpin_kernel.yml` settings:

 * **sculpin_twig.view_paths**:
   List of directories (relative to `source/`) that should be searched for Twig
   templates.
   Default value is `['_views']`.
 * **sculpin_twig.extensions**:
   List of extensions for files that should be used to indicate a file is a Twig
   template.
   Default value is `['', 'twig', 'html', 'html.twig', 'twig.html']`.


## Generators

Generators are used to fabricate new virtual sources based on existing concrete
sources.

A good example of this would be tags or categories for posts. One would not want
to create a tag or category index page for every tag that may ever be created. A
generator can be used to create a tag or category index page dynamically based
on meta data from posts.

Another example would be pagination. If a list of posts needs to be paginated,
one would not want to create an index page for page 1 and page 2 and page 3. One
would prefer to have those pages generated automatically.


## Lifecycle

The following represents the lifecycle of a single pass through all of the
sources.

 * Generate (Generators)
 * Permalink Creation
 * Convert
 * Format
 * Output

For a single "run" (think `sculpin generate`) there is only one run and every
source is considered dirty and needs to be written.

For multiple "runs" (think `scupin generate --watch`) there are many runs. For
the first "run", every source is considered dirty and needs to be written. After
that, each additional "run" will determine whether or not a source is dirty
based on whether it has been updated since the previous run.

### Events

 * **Sculpin\Core\Sculpin::EVENT_BEFORE_RUN**
   Called very early on into the run lifecycle. Suitable for setting up sources
   before anything else is done. Is passed a `SourceSetEvent` instance.
 * **Sculpin\Core\Sculpin::EVENT_AFTER_RUN**
   Called very late into the run lifecycle. Suitable for cleanup. Is passed a
   `SourceSetEvent` instance.
 * **Sculpin\Core\Sculpin::EVENT_BEFORE_CONVERT**
   Called just before a source is converted. Suitable for massaging a source
   prior to converion. Passed a `ConvertEvent` instance.
 * **Sculpin\Core\Sculpin::EVENT_AFTER_CONVERT**
   Called just after a source is converted. Suitable for massaging a source
   after conversion. Passed a `ConvertEvent` instance.
 * **Sculpin\Core\Sculpin::EVENT_BEFORE_FORMAT**
   Called just before a source is formatted. Passed a `FormatEvent` instance.
 * **Sculpin\Core\Sculpin::EVENT_AFTER_FORMAT**
   Called just after a source is formatted. Passed a `FormatEvent instance.

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
[6]: {{site.url}}/documentation/bundles/SculpinPostsBundle/
