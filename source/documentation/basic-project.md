---
title: Basic Project
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

Sculpin reads all files that are under the source directory. Sculpin
expects this directory to be called `source/` in your project root. For
example, if you have a file called `source/index.md`, Sculpin will
generate a file called `output_dev/index.html`.

Besides the actual content, the `index.md` can also provide metadata.
See [Sources]({{site.url}}/documentation/sources/) for the details.

Once created, the `output_prod` folder can be uploaded to a web server
as-is. Because Sculpin is a static site generator, no PHP is used on the
server. This provides greater freedom in hosting choices.

## Commands

### Rendering your Site

The `generate` command looks for files in your source directory and
generates static HTML files:

    vendor/bin/sculpin generate

Your generated web site would then be available in `output_dev`.

The `generate` command has two useful options for editing your site
locally:

* `--watch` will monitor the source directory and regenerate the site
  whenever a source file is changed
* `--server` serves files over HTTP with the built-in webserver

Combining these flags will let you edit your site locally and view the
changes by refreshing your browser.

```
vendor/bin/sculpin generate --watch --server
```

This launches your site in `dev` mode at [localhost:8000](http://localhost:8000)

The `generate` command also has a `--port` option, in case you need the web
server to run on a different port:

    vendor/bin/sculpin generate --watch --server --port=8888

Besides using the `--server` option for `generate`, there are some other
options for previewing the rendered pages locally.

#### Serve Command

To serve files that have already been generated, use the `serve`
command:

    vendor/bin/sculpin serve

This mode will not automatically detect and update changes.

#### Using a Standard Webserver

The only special consideration that needs to be taken into account for standard
webservers **in development** is the fact that the URLs generated may not match
the path at which the site is installed.

This can be solved by overriding the `site.url` configuration option when
generating the site.

    vendor/bin/sculpin generate --url=http://my.dev.host/blog-skeleton/output_dev

With this option passed, `{{ site.url }}/about` will now be generated as
`http://my.dev.host/blog-skelton/output_dev/about` instead of `/about`.

## CSS and JavaScript

It is best practice to combine all your CSS files and all your JavaScript files
into single files. That way they are simple to include in your templates and
create less overhead for the browser loading the page. The recommended way to
combine assets is with Symfony's
[Webpack Encore](https://symfony.com/doc/current/frontend.html).

The [Blog Skeleton](https://github.com/sculpin/sculpin-blog-skeleton) project
uses Encore to manage assets. If you're setting up your project with Sculpin
directly, not using the skeleton, install Encore using the
[setup instructions](https://symfony.com/doc/current/frontend/encore/installation.html).

The rest of this section assumes that you are using Encore, with a
configuration like
[in the skeleton](https://github.com/sculpin/sculpin-blog-skeleton/blob/master/webpack.config.js).

Put your CSS and JS assets in the directory `source/assets/` as shown.

    |-- source/
       `-- assets/
          |-- css/
          |  `-- app.css
          `-- js/
             `-- app.js

The app's main CSS file is configured to be `source/assets/css/app.css`.
You can add more CSS files in the same directory if necessary and require them
in your JavaScript files to use them.

Encore can also support Sass, and the Blog Skeleton is set up to use it. See
the relevant
[Encore docs](https://symfony.com/doc/current/frontend/encore/simple-example.html#using-sass-less-stylus)
for more details.

The app's main JavaScript file is `source/assets/js/app.js`. Make sure that it
is added in the `webpack.config.js` configuration file. You can add further
JavaScript files and require them in `app.js`, and `require` other libraries as
necessary.

Build the assets using the command:

    yarn encore dev --watch

Encore will then compile all the CSS into the `build/app.css` file and all the
JavaScript, including library code, into the `build/app.js` file.

The default templates in the skeleton come with the correct stylesheet link and
script tag. If you build your own templates, add these tags to your base
template  (in `_views/`):

```html
<head>
    <link rel="stylesheet" href="{{ site.url }}/build/app.css">
</head>
<body>
    (all your other content)

    <script src="{{ site.url }}/build/app.js"></script>
</body>
```

## Environments

Sculpin knows the `dev` and `prod` environment. They allow you to have
[different configuration settings by environment](configuration/).

Sculpin assumes that all commands will be run in the `dev` environment
unless otherwise specified.

When you want to build the final web site, run the command with the
`--env=prod` option.

```
vendor/bin/sculpin generate --env=prod
```

The output of this command will be placed in `output_prod`. Upload the
contents of this folder to your public website to deploy your site.
