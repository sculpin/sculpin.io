---
title: Converters
slug: converters

---

Converters will convert incoming markup to something else, generally HTML.
Sculpin ships with two converters, Markdown and Textile.

---

## Markdown Converter

The Markdown Converter will convert `.md`, `.mdown`, `.mkdn` and `.markdown` files
using [michelf/php-markdown](https://packagist.org/packages/michelf/php-markdown).

### Configuration

The Markdown Converter can be configured by adjusting the following
`sculpin_kernel.yml` settings:

 * **sculpin_markdown.parser_class**:
   Can be one of `Sculpin\Bundle\MarkdownBundle\PhpMarkdownExtraParser` or `Sculpin\Bundle\MarkdownBundle\PhpMarkdownExtraParser`. Default value is `Sculpin\Bundle\MarkdownBundle\PhpMarkdownParser`. A custom parser must implement the `Sculpin\Core\Converter\ParserInterface`.
 * **sculpin_markdown.extensions**:
   Default value is `['md', 'mdown', 'mkdn', 'markdown']`.

### Other Markdown Classes

Third party extensions are available to support other Markdown varieties. See the individual package README files for specific installation information.

 * **[Bcremer\Sculpin\Bundle\CommonMarkBundle\SculpinCommonMarkBundle](https://github.com/bcremer/sculpin-commonmark-bundle)** - Bundle that integrates the [league/commonmark](https://github.com/thephpleague/commonmark) markdown parser.

---

## Textile Converter

The Textile Converter will convert `.textile` files using
[netcarver/textile](https://packagist.org/packages/netcarver/textile).

### Configuration

The Textile Converter can be configured by adjusting the following
`sculpin_kernel.yml` settings:

 * **sculpin_textile.extensions**:
   Default value is `['.textile']`.
