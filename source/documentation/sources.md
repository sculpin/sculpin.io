---
title: Sources
slug: sources

---

By default, Sculpin assumes that there will be a directory named `source/` in your project's root folder containing all of the *content* for your site.

If you are working from a project template, such as the Getting Started guide describes, your project will already have a `source` directory. If you are starting your project from scratch, you will need to create a source directory for the content of your site.

    |-- source/

## Source Directories

You may divide your content into sub-directories within the directory `source`. For example, you may want your blog posts to appear with the URL `blog`.

    |-- source/
    |  |-- blog/
    |     |-- 2014-02-21-first-post.md
    |     |-- 2014-03-21-time-management.md
    |  |-- about.md
    |  |-- contact.md

When the HTML files are generated for your site, there will not be a one-to-one correlation between the source files, and the output HTML files. For this reason, you may want to store your source material in a folder with a different name than the output directory. The convention is to use a preceding underscore as this will put the directories alphabetically first. There is no requirement to use this naming convention.

    |-- source/
    |  |-- _posts/
    |  |-- _pages/

If you are using custom content types, using one directory per content type will also allow you to easily apply a custom template for each different content type without having to explicitly state which template the source file should use. This is handy to know about, even if you're not taking advantage of it immediately.

Information on how to map a source directory to a specific output directory is included in the page on [Configuration]({{site.url}}/documentation/configuration/).
    
## Formatting Source Files

Content source files for Sculpin projects are markdown files, with an optional YAML frontmatter header. The YAML frontmatter is delimited
by `---`. For example:

    ---
    title: Hello World
    ---

    This is the content of my page.

Any variables contained in the YAML frontmatter are used, as appropriate, by the view for each content type. As such, the frontmatter is not rendered to the HTML page unless it is explicitly requested by the view template. This means that a page title contained in the YAML frontmatter will not be displayed unless it is explicitly requested by the view for that particular content type. Although you can write plain markdown without the YAML frontmatter, you are advised against doing this as it will omit the HTML element for the page tag `<title>`, which isn't very SEO-friendly.

    # Hello World

    This is the content of my page. But it's not very SEO-friendly because it's missing the HTML element <title>.

There is more information about using frontmatter variables in [Custom Content Types]({{site.url}}/documentation/content-types/custom-types/).


## Rendered Source Files 

Your markdown files will automatically be converted to `.html` files when  generating the output for your site.

For example: let's say you have only one source file, `index.md`:

    |-- source/
       `-- index.md

After generating your content for the dev environment with the command `sculpin generate --watch --server`, you will have the following directory structure:

    |-- source/
       `-- index.md
    |-- output_dev/
       `-- index.html

After generating your content for the **production** environment with the command `sculpin generate --env=prod`, you will have the following directory structure:

    |-- source/
       `-- index.md
    |-- output_dev/
       `-- index.html
    |-- output_prod/
       `-- index.html

You should upload the contents of the directory `output_prod` to your server. You do not need to upload the contents of the source directory, or the developer environment.