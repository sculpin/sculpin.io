---
title: Sources
slug: sources

---

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


## Deep Frontmatter YAML Structures

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
