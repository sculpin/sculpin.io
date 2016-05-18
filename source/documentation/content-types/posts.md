---
title: Posts
slug: content-types/posts

---

Posts are a blog entry style content type that is enabled by default for every
Sculpin project. The default configuration can be seen below:

    sculpin_content_types:
        posts:
            type: path
            path: _posts
            permalink: pretty
            taxonomies:
                - tags
                - categories

Posts will be found in `_posts` inside of your `source` directory. The default
permalink strategy is `pretty` and two taxonomies are supported, `tags` and
`categories`.

In order to override these settings, you can modify
`app/config/sculpin_kernel.yml`. For example, to set the permalink strategy to
something else, you could change your local `sculpin_kernel.yml` to:

    sculpin_content_types:
        posts:
            permalink: blog/:year/:month/:day/:filename/

To disable posts entirely, you would do:

    sculpin_content_types:
        posts:
            enabled: false
