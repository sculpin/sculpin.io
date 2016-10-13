---
title: Basic Sculpin Project
slug: basic-project

---

A Sculpin project is capable of building exactly one static site. By default,
Sculpin assumes a basic filesystem structure for any Sculpin project.

    |-- app/
    |  |-- SculpinKernel.php           # Custom Sculpin kernel
    |  `-- config/
    |     |-- sculpin_kernel.yml       # Sculpin's configuration
    |     |-- sculpin_site.yml         # Site meta data
    |     `-- sculpin_site_${env}.yml  # Env specific meta data
    |-- output_${env}/                 # Env specific generated files
    |-- source/
    |  |-- _posts/                     # Individual blog posts live here
    |  `-- _views/                     # Templates
    `-- composer.json                   # Dependencies

---

## Hello World Project

To get started, try creating a simple "Hello World" project for Sculpin. By
following these rules you can get started with a completely bare Sulpin site in
no time!

### Hello World Directory Structure

The directory structure of a Sculpin project is pretty simple. By default,
Sculpin assumes that there will be a `source/` directory in your project root.
Sculpin will read all of the files in your source directory.

Create a file called `index.md` in your source directory. Sculpin will
automatically translate this file to `index.html` when it generates your site.

Your project should now look like this:

    |-- source/
       `-- index.md

### Smallest Source File

The contents of `index.md` should look like this. We will talk about this in
more detail later in the [Sources]({{site.url}}/documentation/sources/) section.
For now, just type this in exactly.

    ---
    ---

    # Hello World


### Run and View

Your project now has everything Sculpin needs to know in order to generate your
Hello World project. For now, we are going to use the `--watch` and `--server`
flags. This tells Sculpin to *watch* the source directory for changes (so it
can regenerate the site as you edit your files) and to *serve* the site using an
embedded web server.

    vendor/bin/sculpin generate --watch --server

Visit [localhost:8000](http://localhost:8000) to see your new static site!


### Output

The static files are placed in `output_dev`. Explore the `output_dev` directory
to see what is happening behind the scenes:

    |-- output_dev/
    |  `-- index.html
