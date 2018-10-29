---
title: Themes
slug: themes

---

<div class="well well-small">
<h2>WARNING</h2>
<p>
Theme support for Sculpin is still highly experimental. It has been stable in its current form since early 2014 but be aware that the theme API <em>may</em> change drastically over time.
</p>
</div>

A theme is composed of layouts, assets, and views. To create a theme, register your theme name in `sculpin_kernel.yml`:

```yml
# app/config/sculpin_kernel.yml
sculpin_theme:
  theme: myApp/myTheme
```

This configuration would look for a theme in `sources/themes/myApp/myTheme`.

To access theme assets in a twig template, you can use the `theme_path()` template helper. For example {% verbatim %}`{{ theme_path("css/style.css") }}`{% endverbatim %} would resolve to `sources/themes/myApp/css/style.css`.

Themes can also inherit from other themes. To define a theme's parent theme, create a `theme.yml` file in the theme directory.
 
```yml
# sources/themes/myApp/myTheme/theme.yml
parent: 'myApp/parentTheme'
```

Asset resolution for theme layouts, views, and static assets works as follows:

- Check the `sources/` directory
- If the asset is not found, check the theme directory
- If the asset is not found, check the parent theme directory. 


## Example

Consider the following code structure:

```
app/
  config/
    sculpin_kernel.yml
sources/
  index.html.twig
  css/
    page.css
  themes/
    myApp/
      parentTheme/
        _layouts/
          default.html.twig
        images/
          logo.png
      myTheme/
        _layouts/
          default.html.twig
        css/
          style.css
          page.css
```

The `sources/index.html.twig` can work like so:

{% verbatim %}
```twig
---
layout: default
---
{# 
  This view will use the layout from 
  sources/themes/myApp/myTheme/_layouts/default.html.twig,
  which overrides the default layout in parentTheme.
#}

{% block stylesheets %}
  {# 
    This will use a stylesheet from 
    sources/themes/myApp/myTheme/css/style.css 
  #}
  <link rel="stylesheet" href="{{ theme_path("css/style.css") }}" />
  
  {#
    This will use a stylesheet from sources/css/page.css,
    which overrides the page.css in childTheme
  #}
  <link rel="stylesheet" href="{{ theme_path("css/page.css") }}" />
{% endblock}

{% block logo %}
  {#
    This will use an image from 
    sources/themes/myApp/parentTheme/images/logo.png 
  #}
  <img src="{{ theme_path("images/logo.png") }}" />
{% endblock %}
```
{% endverbatim %}


