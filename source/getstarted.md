---
layout: default
title: Get started
nav_name: getstarted

---

# Welcome to Sculpin

This guide will explain the easiest way to get up and published. More features and ways of using Sculpin can be found on the documentation page.

There are four quick steps to follow:

1. Get Sculpin
1. Run Sculpin
1. Use Sculpin
1. Publish your Sculpin site

<hr>

## Get Sculpin

The best way to get Sculpin is to download the PHAR. This is a PHP based command line executable which is used to manage any Sculpin project.

From your command line, use this to download the PHAR file and make it executable.

    curl -O https://download.sculpin.io/sculpin.phar
    chmod +x sculpin.phar

Since it's handy to run Sculpin from any directory you can move it to your bin directory.

    mv sculpin.phar ~/bin/sculpin

You should now be able to type `sculpin` from any directory. If not, you likely do not have your user's bin directory assigned to your shell's `$PATH` variable. On bash, you can fix this by entering:

    PATH=$PATH:$HOME/bin

You will want to add that line into your bash startup scrip also (`.bashrc` or `.bash_profile` in your home directory).

<hr>

## Run Sculpin

Great, you've already installed Sculpin on your system! Sculpin generates a static site from a Sculpin project. The skeleton blog is a great place to start.

Go back to your home directory and download the skeleton:

    cd ~
    git clone https://github.com/sculpin/sculpin-blog-skeleton.git myblog
    cd myblog

Now we must tell Sculpin to install all the project's dependencies from Composer. You will see some JavaScript libraries and other bundles get installed.

    sculpin install

Now we can use Sculpin to generate the blog's static files, watch for changes, and run a local webserver we can use to see the results as we work.

    sculpin generate --watch --server

The `watch` flag tells Sculpin to watch the files for changes, and when changed to re-generate the site automatically. `server` launches PHP's web server which lets you see your work in progress from [localhost:8000](http://localhost:8000).

Please note, the server command may crash from time to time. If this happens, simply re-run the command.

<hr>

## Use Sculpin

Great! You've launched the skeleton blog site!

Your project directory will have an app directory which contains all the logic for generating the blog, an output_dev directory which is not part of the project but contains all the generated static files, a source directory which contains the content of the blog, and some configuration files. Jump right into the source directory.
    cd source

Here you'll see all the components that make up your blog, so lets go ahead and create a new post.

    cd _posts

Lets make a new file here and publish an article in the year 2020:

    touch 2020-01-07-time-travel.md

Using your favorite text editor open up the file and lets write a message in the future!

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

    **So is twig, because it knows this page's name is: {{ page.title }}**

Save the file, and take a look at your site (are you still running `sculpin generate --watch --server` ?)

There you go! With just one file you've updated the blog listing, created a page for the post, and updated the atom feed.

If something didn't generate fully with --watch (like a page for a new tag) re-run the `sculpin generate` command for a full rebuild.

<hr>

## Publish Sculpin

Great! You've installed Sculpin, got a blog running and wrote a new post. Now publish it!

Create a production ready version of your static site:

    sculpin generate --env=prod

This will create a directory `output_prod` in your project's directory which is now ready to be uploaded. Some common options are covered here:

#### rsync to your own server

    rsync -avze 'ssh -p 999' output_prod/ user@example.com:public_html

#### GitHub

GitHub pages change from time to time, it is best to [read their instructions][1].

#### Amazon s3 bucket

The skeleton site comes with a `s3-publish.sh` script which you may edit and use to upload to your bucket.

<hr>

## What's next?

Sculpin is not only for blogs, it can be used to create any number of static site formats. Please read the documentation when ready to do more, and explore the project's code.

Happy coding!


[1]: http://pages.github.com/
