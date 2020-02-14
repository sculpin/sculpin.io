---
title: Internals
slug: internals

---

Internally, Sculpin uses an event-driven architecture to perform its tasks. These
events are fed into Sculpin's Converters, Formatters, and Generators at various 
stages of the [lifecycle][5]. 

## [Converters][1]

[Converters][1] convert incoming markup to something else, generally HTML. Sculpin ships with two converters, Markdown and Textile.

## [Formatters][2]

[Formatters][2] are responsible for formatting sources. This can be considered a view or template layer.

Sculpin ships with one formatter, Twig.

## [Generators][3]

[Generators][3] are used to fabricate new virtual sources based on an existing 
concrete source (e.g., [content type][4]). Sculpin ships with a Pagination generator.

[1]: {{site.url}}/documentation/coverters/
[2]: {{site.url}}/documentation/formatters/
[3]: {{site.url}}/documentation/generators/
[4]: {{site.url}}/documentation/content-types/
[5]: {{site.url}}/documentation/extending-sculpin/lifecycle
