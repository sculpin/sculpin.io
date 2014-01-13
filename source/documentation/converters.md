---
title: Converters
slug: converters

---

Converters will convert incoming markup to something else, generally HTML.
Sculpin ships with two converters, Markdown and Textile.

---

## Markdown Converter

The Markdown Converter will convert `.md`, `.mdown`, and `.markdown` files
using [michelf/php-markdown](https://packagist.org/packages/michelf/php-markdown).

### Configuration

The Markdown Converter can be configured by adjusting the following
`sculpin_kernel.yml` settings:

 * **sculpin_markdown.parser_class**:
   Can be one of `Michelf\MarkdownExtra` or `Michelf\Markdown`. Default value is `Michelf\MarkdownExtra`.
 * **sculpin_markdown.extensions**:
   Default value is `['.md', '.mdown', '.markdown']`.

---

## Textile Converter

The Textile Converter will convert `.textile` files using
[netcarver/textile](https://packagist.org/packages/netcarver/textile).

### Configuration

The Textile Converter can be configured by adjusting the following
`sculpin_kernel.yml` settings:

 * **sculpin_textile.extensions**:
   Default value is `['.textile']`.
