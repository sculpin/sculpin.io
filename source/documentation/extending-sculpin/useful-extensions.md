---
title: Useful Extensions
slug: extending-sculpin/useful-extensions

---

Give your websites and blog posts some pizzazz with these community-built Sculpin extensions.

If you know of an extension that isn't listed here, please let us know!

---

## Icelus Thumbnail Generator

[Icelus][1] uses the [Imanee][2] library to give you a quick and easy Twig tag for generating thumbnails in your posts:

    {% verbatim %} <img src="{% thumbnail('path/to/img.jpg', 150, 150) %}"> {% endverbatim %}

If you're using Composer to manage dependencies, get Icelus by running `composer require beryllium/icelus`. If you're using a sculpin.json file, add the appropriate require statement to your sculpin.json and then run `sculpin update`:

    {
        ...
        "require": {
            "beryllium/icelus": "~1.0.0"
        }
    }

---

### Know of other great extensions, or have you created one of your own?

Announce new extensions on the Sculpin IRC channel (#sculpin on irc.freenode.net), or update this page directly on GitHub.

[1]: https://github.com/beryllium/icelus
[2]: http://imanee.io/