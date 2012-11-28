---
layout: default
title: Documentation

---

# Documentation

Sculpin currently lacks any in-depth or formal documentation. It is currently
"learn by example". If you are interested in trying out Sculpin you should fire
up a Sculpin skeleton site to see Sculpin in action.


## About Skeletons

Skeletons are starting points for a new Sculpin based site. While not strictly
required (you can always start a site from scratch) using a skeleton is a good
way to get a bunch of structure in place with little or no effort.

Unless otherwise noted, the following skeletons are **barebones**. They will
have minimal styles (if any at all) and are not intended to be pretty. You are
expected to add all of the style magic yourself.

Read another way, these are simply reference sites that you can scour for ideas
on how to accomplish various things with your own site. Feel free to use as much,
or as little, of these skeletons as you like.


## Composer

The easiest way to get started with a skeleton is by using [Composer][1]. If
you are not familiar with it, get familiar with it. Besides being **awesome**,
Sculpin relies on it pretty heavily.

Please see the installation instructions for [*nix][2] and [Windows][3] to get
Composer installed.

For the rest of these examples we will assume that you have Composer available
as `composer` on your path. If you opt to not install Composer globally use
`php composer.phar` in place of `composer` anytime you see `composer` in the
following commands.


## Blog Skeleton

The blog skeleton ([sculpin/blog-skeleton][4]) sets up a very basic Sculpin
based blog. Once created you will find the following features:

 * A handful of existing posts in `source/_posts/` to get you started. Feel
   free to remove these when you are ready.
 * An about page at `/about`.
 * An index page at `/`. It displays all posts and paginates them.
 * A blog archive page at `/blog`. It displays post titles broken down by
   month and is paginated.
 * A blog tags page at `/blog/tags`.
 * A blog tag index at `/blog/tags/$tag`. Similar to the blog archive
   except broken down by each tag.
 * A GitHub Gist extension is enabled to support {{ '{{ gist($GIST_ID) }}' }}
   in posts.

### Installation

    composer create-project sculpin/blog-skeleton -n -s dev sculpin-blog
    cd sculpin-blog
    vendor/bin/sculpin generate --watch --server

Your newly generated blog is now accessible at `http://localhost:8000/`.


## Questions?

Check out the Sculpin [community]({{site.url}}/community) if you have questions.


[1]: http://getcomposer.org
[2]: http://getcomposer.org/doc/00-intro.md#installation-nix
[3]: http://getcomposer.org/doc/00-intro.md#installation-windows
[4]: https://packagist.org/packages/sculpin/blog-skeleton