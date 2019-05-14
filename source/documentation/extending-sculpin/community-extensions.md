---
title: Community Extensions
slug: extending-sculpin/community-extensions

---

Community-made extensions are a great way to extend the capabilities of
your Sculpin site.

<blockquote>
Know of an extension that belongs on this list? Send a Pull
Request to the <a href="https://github.com/sculpin/sculpin.io">
sculpin.io</a> repository on GitHub, or reach out to <strong><a
href="https://twitter.com/getsculpin">@getsculpin</a></strong> on
Twitter!
</blockquote>

**[Meta Navigation Bundle](https://packagist.org/packages/janbuecker/sculpin-meta-navigation-bundle)**

This extension helps you build navigation menus for your site.

To make a menu item visible, add a `menu_title` entry to the page's
front matter.

Then, loop on `page.menu` to produce your menu, allowing up to
3 levels of depth.

**[Icelus Thumbnail Generator](https://packagist.org/packages/beryllium/icelus)**

Generate thumbnails from within Twig:

```
{% verbatim %}
<a href="image.jpg"><img src="{{ thumbnail('image.jpg', 100, 100) }}"></a>
{% endverbatim %}
```

**[Related Posts Bundle](https://packagist.org/packages/tsphethean/sculpin-related-posts-bundle)**

List five related posts (based on tag and category correlations) below
any given post:

```
{% verbatim %}
{% if page.related %}
<ul>
  {% for relate in page.related %}
  <li><a href="{{ relate.source.url }}">{{ relate.title }}</a></li>
  {% endfor %}
</ul>
{% endif %}
{% endverbatim %}
```

**[Twig Markdown Bundle](https://packagist.org/packages/opdavies/sculpin-twig-markdown-bundle)**

Process markdown strings from within Twig:

```
{% verbatim %}
{{ some_content|markdown }}
{% endverbatim %}
```

**[Sort By Field Bundle](https://packagist.org/packages/opdavies/sculpin-twig-sort-by-field-bundle)**

From within Twig, allows you to sort arrays by key:

```
{% verbatim %}
{% for i in myArray | sortbyfield('array_sort_key') %}
  {{ i.array_sort_key }}
{% endfor %}
{% endverbatim %}
```