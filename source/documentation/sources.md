---
title: Sources
slug: sources

---

By default, Sculpin assumes that there will be a directory named
`source/` in your project's root folder containing all of the *content*
for your site.

In addition to the actual content, these files can provide a YAML
frontmatter. Sources that have YAML frontmatter are considered special
in that they can be formatted using Twig and other formatters.

If you are working from a project template, as the Getting Started guide
describes, your project will already have a `source` directory. If you
are starting your project from scratch, you will need to create a source
directory for the content of your site.

    |-- source/

This can be easily done using the new `sculpin init` command.

## Source Directories

You may divide your content into sub-directories within the directory
`source`. For example, you may want to have some custom pages in a
folder named "stories":

    |-- source/
    |  |-- stories/
    |     |-- the-fox-and-the-greyhound.md
    |     |-- scalar-morghulis.md
    |  |-- about.md
    |  |-- contact.md

Entries that are related to Content Types will be stored in a special
subdirectory, such as blog posts being stored in `_posts/`. When Sculpin
generates the content, these content type files will be converted to
live at the location specified by the content type's URL configuration.

## What Is YAML Frontmatter?

As said above, sources that have YAML frontmatter are considered special
in that they can be formatted using Twig and other formatters.

A file without YAML frontmatter looks like this:

```
# This is a markdown file without YAML frontmatter
```

Whereas a file with YAML frontmatter looks like this:

```
---
layout: default
---

# This is a markdown file with YAML frontmatter
```

The frontmatter is the chunk of YAML in the second example. It is delimited
by `---`. The YAML frontmatter is parsed and injected into every page rendering
and is accessible as `page.KEY`.

### Nested Frontmatter YAML Structures

Sculpin reads nested structures in YAML frontmatter. Use a `.` to
indicate that you want to descend into a structure. For example:

    ---
    layout: default
    something:
        here:
            very: deep
            also: deep
    ---

    {% verbatim %}We can reference `{{ page.something.here.also }} === deep`.{% endverbatim %}

## Formatting Source Files

Content source files for Sculpin projects are markdown files, with an
optional YAML frontmatter header. As shown above, the YAML frontmatter
is delimited by `---`. For example:

    ---
    title: Hello World
    ---

    This is the content of my page.

Any variables contained in the YAML frontmatter are used, as appropriate, by the view for each content type. As such, the frontmatter is not rendered to the HTML page unless it is explicitly requested by the view template. This means that a page title contained in the YAML frontmatter will not be displayed unless it is explicitly requested by the view for that particular content type. Although you can write plain markdown without the YAML frontmatter, you are advised against doing this as it will omit the HTML element for the page tag `<title>`, which isn't very SEO-friendly.

    # Hello World

    This is the content of my page. But it's not very SEO-friendly because it's missing the HTML element <title>.

There is more information about using frontmatter variables in [Custom Content Types]({{site.url}}/documentation/content-types/custom-types/).


## Rendered Source Files 

Your markdown files will automatically be converted to `.html` files when  generating the output for your site.

For example: let's say you have only one source file, `index.md`:

    |-- source/
       `-- index.md

After generating your content for the dev environment with the command `sculpin generate --watch --server`, you will have the following directory structure:

    |-- source/
       `-- index.md
    |-- output_dev/
       `-- index.html

After generating your content for the **production** environment with the command `sculpin generate --env=prod`, you will have the following directory structure:

    |-- source/
       `-- index.md
    |-- output_dev/
       `-- index.html
    |-- output_prod/
       `-- index.html

You should upload the contents of the directory `output_prod` to your server. You do not need to upload the contents of the source directory, or the developer environment.