---
title: Layouts
slug: layouts

---

With Sculpin, a layout is more or less a wrapper or shell around your pages
content. Layouts can technically live in any of the view directories
(`_views`, `_layouts`, `_partials`, `_includes`) but for the sake of consistency
it is best to place them either in `_views` (if you only ever use the `_views`
directory for all of your templates) or in `_layouts`.

For a layout to work, it must be able to render a Source's `content` block. For
a Twig template, that means:

    {% verbatim %}{% {% endverbatim %}block content{% verbatim %} %}{% endverbatim %}{% verbatim %}{% {% endverbatim %}endblock{% verbatim %} %}{% endverbatim %}

... or ...

    {% verbatim %}{{ page.blocks.content }}{% endverbatim %}

---

## Inheritance and Sources

Many static site generators, including Jekyll and Phrozn, will render each
source first, and inject the resulting output into the layout. While this
approach (the "russian dolls" approach) is simpler, it means you end up losing
the inheritance capabilities that are built into both Twig and Liquid.

Sculpin attempts to solve this problem by wrapping each source in a block named
`content`. So, given the following file:

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



