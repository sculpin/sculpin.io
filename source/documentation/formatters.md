---
title: Formatters
slug: formatters

---


Formatters are responsible for formatting sources. This can be considered a view
or template layer.

Sculpin ships with one formatter, Twig.

---

## Twig Formatter

The Twig Formatter is responsible for laying out individual sources into nicer
"complete" files. Most of the time this will be formatting into an HTML file but
there are definitely cases when files will be formatted as CSS, JavaScript, or
XML (Atom or RSS).


### Configuration

The Twig Formatter can be configured by adjusting the following
`sculpin_kernel.yml` settings:

 * **sculpin_twig.view_paths**:
   List of directories (relative to `source/`) that should be searched for Twig
   templates.
   Default value is `['_views', '_layouts', '_partials', '_includes']`.
 * **sculpin_twig.extensions**:
   List of extensions for files that should be used to indicate a file is a Twig
   template.
   Default value is `['', 'twig', 'html', 'html.twig', 'twig.html']`.
