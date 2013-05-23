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


## Blog Skeleton

The blog skeleton sets up a very basic Sculpin based blog. Once created you will
find the following features:

 * Very minimal Bootstrap based theme.
 * A handful of existing posts in `source/_posts/` to get you started. Feel
   free to remove these when you are ready.
 * An about page at `/about`.
 * An index page at `/`. It displays all posts and paginates them.
 * A blog archive page at `/blog`. It displays post titles broken down by
   month and is paginated.
 * A blog categories page at `/blog/categories`.
 * A blog category index at `/blog/categories/$category`. Similar to the blog
   archive except broken down by each category.
 * A blog tags page at `/blog/tags`.
 * A blog tag index at `/blog/tags/$tag`. Similar to the blog archive
   except broken down by each tag.

### Installation

First, fork and/or clone the project. ([see project on GitHub](https://github.com/sculpin/sculpin-blog-skeleton))

    git clone https://github.com/sculpin/sculpin-blog-skeleton.git

Then...

#### If You Already Have Sculpin

    sculpin install
    sculpin generate --watch --server

Your newly generated blog is now accessible at `http://localhost:8000/`.

#### If You Need Sculpin

    curl -sS https://sculpin.io/installer | php
    php sculpin.phar install
    php sculpin.phar generate --watch --server


## Questions?

Check out the Sculpin [community]({{site.url}}/community) if you have questions.


[1]: http://getcomposer.org
[2]: http://getcomposer.org/doc/00-intro.md#installation-nix
[3]: http://getcomposer.org/doc/00-intro.md#installation-windows
