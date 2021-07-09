---
layout: default
title: sculpin_kernel.yml

---

# sculpin_kernel.yml

Some parts of Sculpin, specifically anything configured as a bundle, must be
configured at the kernel level. This can be done by modifying the
`sculpin_kernel.yml` file.

    |-- app/
    |  `-- config/
    |     `-- sculpin_kernel.yml       # Sculpin's configuration (optional)


For example, to configure something like the default permalink for posts, one
would need to configure the posts bundle's configuration:

    sculpin_posts:
        permalink: blog/:year/:month/:day/:filename/

Or if one wanted to change the default Markdown parser class, one would:

    sculpin_markdown:
        parser_class: Michelf\Markdown

## Additional Examples

Here is an incomplete list of of example overrides that can be done through sculpin_kernel.yml

~~~
sculpin:
  # Paths marked as 'raw' are not processed by Sculpin at all and are copied
  # straight to the output directory. The "raw" designation is useful in case
  # something like compressed javascript or compressed css that would otherwise
  # be mangled.
  raw:
    - "path/to/raw/code"
    - "another/directory/of/raw/code"
  # Excluded files are not copied to the output directory yet still trigger
  # a rebuild out the output site. The Twig bundle adds the '_views' directory
  # to this list because these files do not need to be on a production website
  # yet changes to those files alter the output of the site.
  exclude:
    # Sass code doesn't need to be sent to the live server.
    - "code/_sass/"
    # @todo I don't know why the "*" is needed in this path to make the file
    # actually be excluded but it is.
    - "code/config.rb*"
  # Paths marked as "ignore" will be ignored by Sculpin and not copied to the
  # output directory. Unlike "exclude," changes to paths under "ignore" will not
  # trigger Sculpin rebuilds.
  ignore:
  - "ignore/this/directory"
  - "ignore/this/pattern_*"
~~~
