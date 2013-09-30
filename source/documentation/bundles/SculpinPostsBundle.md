---
layout: default
title: SculpinPostsBundle

---

SculpinPostsBundle
==================

The default behavior of Sculpin is that no one source has any meaning over any
other Source.  [PostsBundle](https://github.com/sculpin/posts-bundle) allows for
treating some sources as if they are Posts. For all intents and purposes, it
adds blogging capabilities to Sculpin.


Installation
------------

The bundle should be included in Sculpin and enabled by default.

If you are building your own custom Sculpin from the ground up, you need to
require either [sculpin/sculpin](https://packagist.org/packages/sculpin/sculpin)
or [sculpin/posts-bundle](https://packagist.org/packages/sculpin/posts-bundle)
via [Composer](https://getcomposer.org/) and you need to ensure that
`Sculpin\Bundle\PostsBundle\SculpinPostsBundle` is registered.


Configuration
-------------

The default configuration is as follow:

~~~yaml
sculpin_posts:
    paths: ["_posts"]
    publish_drafts: null
    permalink: pretty
    layout: post
~~~


### paths

Paths is a list of directories in which sources should be considered Posts.
default setting is `["_posts"]` which means any source under `sources/_posts`
will be considered a Post.


### publish_drafts

Posts may be considered draft if they have a `draft` top level metadata key in
their YAML frontmatter.

The default behavior is that if `publish_drafts` is not set (`null`) it will be
set based on the Kernel's environment. If the environment is `prod`, the value
is set to `false`. In all other cases, the value is set to `true`.

The end result is that in the default `dev` environment drafts will be
published. If `---env=prod` is specified, drafts will not be published.

If drafts are set to be published, any Post that is marked as draft will
automatically be tagged with the "drafts" tag.


### permalink

The default permalink to use if one is not specified by the source itself.
Defaults to `pretty`.

To use a common date based format, you could set the permalink to something
like:

    blog/:year/:month/:day/:filename/


### layout

The default layout to use if one is not specified by the source itself. Defaults
to `post`.


Post
----

A Post is a tiny wrapper over a `ProxySource`. A `ProxySource` is a more
view-friendly interface around a `SourceInterface`. The Post wrapper provides a
little bit of extra functionality specific to posts.


### Drafts

A Post may be marked as draft by setting the `drafts` top level metadata key to
`true`. A Post with this setting will be treated as a draft and subject to the
`publish_drafts` rules listed above.

    ---
    draft: true
    title: This is a WIP
    ---
    # More to come later


If a draft Post is published it will automatically have the "drafts" tag added
to it.


### Title

A Post has a title as a first class concept. It is set by the `title` top level
metadata key. If a Post is used from a data provider, title can be easily found
by requesting `post.title`.

This is simply a shortcut for `post.meta.title`.

Example:

    ---
    title: The Best Title Ever
    ---
    # Hello World

### Date

A Post has a notion of a date. It is a "calculated" value based on either
information in the filename ("YYYY-MM-DD-rest-of-filename.md") or read from the
`date` top level metadata key. If a Post is used from a data provider, date can
be easily found by requesting `post.date`.

Example of a date being specified by YAML frontmatter:

    ---
    title: The Best Title Ever
    date: 2013-09-29 20:05
    ---
    # Hello World

Example of a date being specified by a filename (example,
"2013-09-29-the-best-title-ever.md"):

    ---
    title: The Best Title Ever
    ---
    # Hello World

### Tags and Categories

Posts have special support for tags and categories. These can be added to a post
by including `tags` and `categories` top level metadata keys.

    ---
    title: The Best Title Ever
    tags: ["simple", "example", "php"]
    categories: ["opinion", "software"]
    ---
    # Hello World


### Previous Post and Next Post

A Post has a concept of the Post that comes before and after it. These are set
as a part of the Posts initialization. They are available as `post.nextPost` and
`post.previousPost`. They will be `null` where appropriate.

These are also available via metadata by accessing `post.meta.next_post` and
`post.meta.previous_post`.


Posts DataProvider
------------------

Posts can be injected into any source by using them with `use: ["posts"]`.

    ---
    use:
        - posts
    ---
    {% for post in data.posts %}
        <article>
            <div class="title">{{ post.title }}</div>
            <div class="content">{{ post.blocks.content|raw }}</div>
            {% if post.meta.external_link %}
                <a href="{{ post.meta.external_link }}">External Link</a>
            {% endif %}
        </article>
    {% endfor %}


DataProvider provided data behaves in a way that is similar to a standard source
but there are a few differences.

First, standard YAML frontmatter is accessible via `post.meta`. Second, in order
to get access to the content for the source, its appropriate block must be
access like `post.blocks.content`.


Extending Posts Behavior with a Map
-----------------------------------

A custom Map can be applied to posts by registering a service that implements
`Sculpin\Core\Source\MapInterface` that is tagged with
`sculpin_posts.posts_map`.

A trivial example would be a map that looks at the title of every post and
automatically tags important words. The use case would be that if you write
about Silex very often and want to ensure that every post with the word Silex in
the title has the silex tag even if you forget.

### AutoTagFromTitle Class

This is a trivial implementation of a Sculpin Source Map. Every Source that is
determined to be a post will be sent to this service.

~~~php
namespace Acme\SculpinBlog;

use Sculpin\Core\Source\Map\MapInterface;
use Sculpin\Core\Source\SourceInterface;

class AutoTagFromTitleMap implements MapInterface
{
    private $tags;

    public function __construct(array $tags = array())
    {
        $this->tags = array_map(function ($value) {
            return strtolower($value);
        }, $tags);
    }

    public function process(SourceInterface $source)
    {
        $tags = array();

        // Break out the title into words.
        $nameParts = explode(' ', $source->data()->get('title'));

        foreach ($nameParts as $name) {
            if (in_array(strtolower($name), $this->tags)) {
                // If this is a word we care about, we should add
                // it to our tags list.
                $tags[] = strtolower($name);
            }
        }

        $existingTags = $source->data()->get('tags');
        if (null === $existingTags) {
            // The Post had no tags to begin with
            $existingTags = array();
        } else {
            if (!is_array($existingTags)) {
                if ($existingTags) {
                    // Normalize in case people did something
                    // not smart.
                    $existingTags = array($existingTags);
                } else {
                    // Just in case...
                    $existingTags = array();
                }
            }
        }

        // Combine the tags we added with the existing tags making
        // sure that we do not duplicate tags.
        $source->data()->set('tags', array_unique(array_merge(
            $tags,
            $existingTags
        )));
    }
}
~~~


### Register the Service

This can be handled in any number of ways. The best way would probably be to
publish it as a bundle and require it with `sculpin.json` or `composer.json`.
For the sake of brevity, we'll show an example of loading this through
`sculpin_services.yml` just to show how to wire up the service.

~~~yaml
#
# app/config/sculpin_services.yml
#

parameters:
services:
    acme_sculpin_blog_auto_tag_from_title_map:
        class: Acme\SculpinBlog\AutoTagFromTitleMap
        arguments:
            - ["yolo", "silex", "symfony"]
        tags:
            - { name: sculpin_posts.posts_map }
~~~
