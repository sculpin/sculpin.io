---
layout: doc
title: Get Started
nav_name: getstarted
slug: get-started

---

## Welcome to Sculpin!

In this guide you'll learn the easiest way to get up and published using a blog template. Sculpin is not only for blogs, it can be used to create any number of static site formats, this is just a starting place to show you what's possible.

To create and publish your first Sculpin site, you will need to complete the following steps:

1. Download and Install Sculpin
1. Download and Install a Starter Kit
1. Run Sculpin
1. Add Content to Sculpin
1. Generate a Production-Ready Site
1. Deploy Sculpin

---

## Download and Install Sculpin

The best way to get Sculpin is to download the PHAR. This is a PHP based command line executable which is used to manage any Sculpin project.

From your command line, use this to download the PHAR file and make it executable.

    curl -O https://download.sculpin.io/sculpin.phar
    chmod +x sculpin.phar

Since it's handy to run Sculpin from any directory you can move it to your bin directory.

    mv sculpin.phar ~/bin/sculpin

You should now be able to type `sculpin` from any directory. If not, you likely do not have your user's bin directory assigned to your shell's `$PATH` variable. On bash, you can fix this by entering:

    PATH=$PATH:$HOME/bin

You will want to add that line into your bash startup scrip also (`.bashrc` or `.bash_profile` in your home directory).

## Download and Install a Starter Kit

One of the most popular ways to use Sculpin is as a blogging platform. (This use of Sculpin is similar to using the blogging tool Jekyll.) The blog starter kit isn't included in the Sculpin project because Sculpin itself is not limited to a blogging platform. As a result, you will need to download this starter kit separately. The remainder of this tutorial assumes you have this starter kit in place, so please complete the following steps as well.

Download the starter kit from GitHub:

    cd ~
    git clone https://github.com/sculpin/sculpin-blog-skeleton.git myblog
    cd myblog

You will notice several configuration files in the main directory for your project as well as the following directories:

- `app` contains all the logic for generating the blog.
- `source` contains the raw content for your blog.

Now we must tell Sculpin to install any relevant dependencies for your project. You will see some JavaScript libraries and other bundles get installed. You must run this command for each new project you start! Make sure you are in the root directory for your project, and then run the install command.

    cd ~/myblog
    sculpin install

You are now ready to start the server, and add content to your new Sculpin site.

---

## Run Sculpin

Now we can use Sculpin to generate static files, watch for changes, and run a local web server we can use to see the results as we work.

    sculpin generate --watch --server

The `watch` flag tells Sculpin to watch the files for changes, and when changed to re-generate the site automatically. `server` launches PHP's web server which lets you see your work in progress from [localhost:8000](http://localhost:8000). After having run this command, a new directory, `output_dev`, will appear in your project, folder.

Please note, the server command may crash from time to time. If this happens, simply re-run the command.

---

## Add Content to Sculpin

You are now ready to add blog posts to your new site. Your blog posts will be in Markdown format, and contain metadata in YAML format. (Don't worry, it's easy.)

Jump right into the source directory.

    cd source

Here you'll see all the components that make up your blog, so let's go ahead and create a new post.

    cd _posts

Let's make a new file here and publish an article in the year 2020:

    touch 2020-01-07-time-travel.md

Using your favorite text editor open up the file and let's write a message in the future!

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

With this one file you've updated the blog listing, created a page for the post, and updated the atom feed.

Assuming you are still running the server with the command `sculpin generate --watch --server`, the new pages are now available on your local server ([localhost:8000](http://localhost:8000)). You will need to refresh the browser to see your new content.

If the content hasn't generated fully (perhaps there is a page missing for one of the tags). Simply stop and then restart the server from the command line:

    control-C
    sculpin generate --watch --server

---

## Generate a Production-Ready Site

Great! You've installed Sculpin, got a blog running and wrote a new post. Now publish it!

Create a production ready version of your static site:

    sculpin generate --env=prod

This will create the directory `output_prod` in your project's directory. The contents of this file can now be uploaded.

---

## Deploy Sculpin

In the previous step you created a stand-alone version of your site built from static HTML files. These files, which reside in `output_prod`, need to be uploaded to your publicly accessible web server.

Some common options are covered here:

#### rsync to your own server

    rsync -avze 'ssh -p 999' output_prod/ user@example.com:public_html

#### GitHub

GitHub pages change from time to time, it is best to [read their instructions][1].

#### Amazon s3 bucket

The skeleton site comes with a `s3-publish.sh` script which you may edit and use to upload to your bucket.

---

## What's next?

Now that you have created your first Sculpin site, you are ready to dive into creating highly customized sites. You may want to proceed by looking at [what others have built](../community), or you may want to dive into the [Sculpin documentation](../documentation).

[1]: http://pages.github.com/
