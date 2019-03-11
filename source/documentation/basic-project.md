---
title: Basic Sculpin Project
slug: basic-project

---

A Sculpin project is capable of building exactly one static site. By default,
Sculpin is configured to work with the following file structure:

    |-- app/
    |  |-- SculpinKernel.php           # Custom Sculpin kernel
    |  `-- config/
    |     |-- sculpin_kernel.yml       # Sculpin's configuration
    |     |-- sculpin_site.yml         # Site meta data
    |     `-- sculpin_site_${env}.yml  # Env specific meta data
    |-- output_${env}/                 # Env specific generated files
    |-- source/                        # Files in here are read and compiled
    |  |-- _posts/                     # Individual blog posts live here
    |  `-- _views/                     # Templates
    `-- composer.json                  # Dependencies

---

Sculpin reads all files that are under the source directory. By default, this
directory is called `source/` in your project root. For example, if you have a
file called `source/index.md`, Sculpin will generate an
`index.html` file in the output directory for you.

Besides the actual content, the `index.md` can also provide metadata. See
[Sources]({{site.url}}/documentation/sources/) for the details.

The output folder can be uploaded to a web server as is. Because Sculpin is a
static site generator, no PHP is used on the server.

## Commands

### Rendering your Site

The `generate` command looks for files in your source directory and generates
static HTML files:

    vendor/bin/sculpin generate

Your generated web site is now available in `output_dev`.

The `generate` command has two useful options:

* `--watch` monitor the source directory and regenerate the site whenever a
  source file is changed;
* `--server` to serve files over HTTP with the built-in webserver.

    vendor/bin/sculpin generate --watch --server

Visit [localhost:8000](http://localhost:8000) to see your new static site!

The `generate` command also has a `--port` option, in case you need the web
server to run on a different port:

    vendor/bin/sculpin generate --watch --server --port=8888

Besides using the `--server` option for `generate`, you have the following
options for previewing the rendered pages locally.

#### Serve Command

To serve files that have already been generated, use the `serve` command:

    vendor/bin/sculpin serve

#### Using a Standard Webserver

The only special consideration that needs to be taken into account for standard
webservers **in development** is the fact that the URLs generated may not match
the path at which the site is installed.

This can be solved by overriding the `site.url` configuration option when
generating the site.

    sculpin generate --url=http://my.dev.host/blog-skeleton/output_dev

With this option passed, `{{ site.url }}/about` will now be generated as
`http://my.dev.host/blog-skelton/output_dev/about` instead of `/about`.

## Environments

Sculpin knows the `dev` and `prod` environment. They allow you to have
[different configuration settings by environment](configuration/). By default,
the `dev` environment is used.

When you want to build the final web site, run the command with the `--env=prod`
option. The output of this command will be placed in `output_prod`. Upload the
contents of this folder to your public website.
