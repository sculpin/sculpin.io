---
layout: doc
title: Get Started
nav_name: getstarted
slug: get-started

---

## Welcome to Sculpin!

In this guide, you'll be introduced to the Sculpin Blog Skeleton. You'll
download and install it, run it, add some content to it, and generate
and deploy a production-ready site using it.

Sculpin can be used to create any type of static website. The blog
skeleton is a good way to explore Sculpin's features and get accustomed
to working with it.

To create and publish your first Sculpin site, you'll be guided through
the following steps:

1. Downloading and Installing Composer
1. Starting a Blog
1. Running Sculpin
1. Adding Content to Sculpin
1. Running Yarn
1. Personalizing Your Site
1. Generating a Production-Ready Site
1. Deploying Static Sites

---

## Download and Install Composer

Sculpin relies on Composer for installation. Composer is a PHP based
package management tool which is used to manage Sculpin's dependencies.

> Use the instructions on the [Composer download page](https://getcomposer.org/download/)
to get started. The provided commands include steps that verify the
installer's signature, so they can't be copied and pasted here.

It's handy to be able to run Composer from any directory, which you can
do by adding it to a folder in your path. For example, if your home
directory contains a "bin" folder that is in your path, you could move
composer like so:

    mv composer.phar ~/bin/composer

You would now be able to type `composer` from any directory. If that
turns out not to work, you likely do not have your user's bin directory
assigned to your shell's `$PATH` variable. Using the bash shell, you can
fix this by entering:

    PATH=$PATH:$HOME/bin

<small>Rather than entering that every time, you can add that line into your
bash startup script also (`.bashrc` or `.bash_profile` in your home
directory).</small>

## Starting a Blog

One of the most popular ways to use Sculpin is as a blogging platform.
This use of Sculpin is similar to other blogging tools, such as Jekyll
or Hugo. Sculpin itself is not limited to being a blog, it can be used
for any type of static website, which is why this specifically-tuned
"blog skeleton" is provided separately from the main project.

Using composer, create a new blog:

    composer create-project sculpin/blog-skeleton myblog
    cd myblog

When Composer asks if you want to remove existing VCS files, go ahead
and answer "Yes". You can run `git init` later to start version-tracking
your content.

You will notice several configuration files in the main directory for
your project as well as the following directories:

- `app/` contains some of the logic for generating the blog.
- `source/` contains the raw content for your blog.

Composer's create-project command has now installed the relevant PHP
dependencies for your project.

You are now ready to start the server and add content to your new
Sculpin blog.

---

## Run Sculpin

Now we can use Sculpin to generate static files, watch for changes, and
run a local web server to see the results as we work.

    vendor/bin/sculpin generate --watch --server

The `--watch` flag tells Sculpin to watch the files for changes, and
when changed to re-generate the site automatically. The `--server` flag
launches PHP's web server which lets you see your work in progress from
[localhost:8000](http://localhost:8000).

After having run this command, a new directory, `output_dev`, will
appear in your project folder.

The `generate` command also takes a `--port` option to run on a
different port, in case the default is currently being used:

    vendor/bin/sculpin generate --watch --server --port=8888

There's also a helpful shortcut that leverages Composer to make things
easier to remember:

```
composer sculpin-watch
```

Please note, the server command may encounter exceptions from time to
time. This can happen if your editor saves a file before you're finished
typing a complex templating tag. The generate command will catch these
exceptions and provide information about what file and line number the
issue was observed on.

---

## Add Content to Sculpin

You are now ready to add blog posts to your new site. Your blog posts
will be in Markdown format, and contain metadata in YAML format. (Don't
worry, we explain this all in detail.)

Jump right into the source directory.

    cd source

Here you'll see all the components that make up your blog, so let's go
ahead and create a new post.

    cd _posts

Let's make a new file here and publish an article in the year 2020:

    touch 2020-07-19-time-travel.md

Using your favorite text editor open up the file and let's write a
message in the future!

    ---
    title: Time travel
    tags:
        - future
        - time
    categories:
        - time
    ---

    # Hello world.

    I am in the future.

    *Markdown is cool.*

    {% verbatim %}**So is twig, because it knows this page's name is: {{ page.title }}**{% endverbatim %}

Save the file.

With this one file you've updated the blog listing, created a page for
the post, and updated the atom feed.

Assuming you are still running the server with the command
`sculpin generate --watch --server`, the new pages are now available on
your local server ([localhost:8000](http://localhost:8000)). You will
need to refresh the browser to see your new content.

If the content hasn't generated fully (perhaps there is a page missing
for one of the tags), you can stop and then restart the server from the
command line:

    control-C
    vendor/bin/sculpin generate --watch --server

Your blog post should now show up on the site. You can also see the
generated file at

    output_dev/blog/2020/01/07/time-travel/index.html

---

## Run Yarn

When you're ready to start modifying your CSS and JS to personalize the
look and feel of your blog, you can choose to go your own way and do
things by hand. Or, you can install the `yarn` tool for compiling
changes to CSS and JS. The skeleton comes preconfigured for the Webpack
and Encore tools to deliver a modern toolchain for frontend development.

> These [installation instructions for Yarn](https://yarnpkg.com/en/docs/install)
will guide you to the proper steps for your system.

Once yarn is installed, these commands will get you started:

    yarn install
    yarn encore dev --watch

The watch command can also be launched from Composer:

    composer yarn-watch

Yarn will watch for changes to CSS and JS files and regenerate the
streamlined assets to incorporate the new changes.

> To run the Sculpin watch process at the same time as the Yarn watch
process, it's advised to start a second terminal window and run the Yarn
command there.

---

## Personalize Your Site

Assets for your site are stored under `source/assets/`. When Yarn
detects changes to the below files, it will then assemble them into some
build artifacts in the `source/build/` folder. These build artifacts are
what are downloaded when your site is loaded.

### `source/assets/css/app.scss`

This file contains a number of SCSS ("Sassy CSS") directives. Yarn will
run these through the SCSS preprocessor to create the build artifacts.

### `source/assets/js/app.js`

This file is where your site's JS will live. You can use all kinds of
wizardry here if you're so inclined; Yarn will happily assemble it into
a build artifact.

---

## Generate a Production-Ready Site

Great! You've installed Sculpin, got a blog running, personalized it,
and written a new post. Now publish it!

Create a production ready version of your static site:

    vendor/bin/sculpin generate --env=prod

This will create the directory `output_prod` in your project's
directory. The contents of this directory are ready to be uploaded to a
webserver.

> The main purpose of the "prod" environment is to hide draft blog posts
and pages.

---

## Deploy your Generated Site

In the previous step you created a stand-alone version of your site
built from static HTML files. These files, which reside in
`output_prod`, need to be uploaded to your publicly-accessible web
server.

Some common options are covered here:

#### rsync to your own server

    rsync -avze 'ssh -p 999' output_prod/ user@example.com:public_html

You might want to use the `--delete` option to also delete files that
got removed. Always make sure that there are no other files in the
target directory that you do not want to be deleted. When in doubt, try
with the `--dry-run`/`-n` flag first and check what rsync would do.

#### GitHub

For GitHub pages, you will commit the rendered files in a git
repository. Please refer to the official
[instructions on GitHub pages][1].

#### Amazon S3 bucket

The skeleton site comes with a `s3-publish.sh` script which you may edit
and use to upload to your bucket. You will need to install the `s3cmd`
utility in your system for this script to work.

---

## What's next?

Now that you have created your first Sculpin site, you are ready to dive
into creating highly customized sites. You may want to proceed by
looking at [what others have built](../community), or you may want to
explore the [Sculpin documentation](../documentation).

[1]: http://pages.github.com/
