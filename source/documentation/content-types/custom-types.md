---
title: Custom Types
slug: content-types/custom-types

---

You can create your own custom content types with Sculpin. To do so,
configure `sculpin_content_types` in `app/config/sculpin_kernel.yml` by
following the guidelines outlined below.

The end result will be one or more data providers and optionally some
taxonomy-related data providers (like "tags" on blog posts) and index
generators.

The content types bundle uses rules to derive some values automatically
so that you have to configure fewer things. Everything can be
overridden, though, so you can tailor the configuration if you're not
satisfied by Sculpin's default guesses.

---

## Configuration

Content types are defined by configuring the `sculpin_content_types`
section of `app/config/sculpin_kernel.yml`. The top level keys in this
node are considered the type names. Each type can have additional
configuration.

### Type Configuration Keys

For a given type name (the keys in the `sculpin_content_types`
configuration), the following keys are available:

 * **singular_name**:
   The singularized name for the type. Defaults to the result of calling
   a singularize function on the type name.
 * **type**:
   The type of content type, either **path** or **meta**. Essentially,
   this is how Sculpin determines *how* it will select the content type.
   Either based on path or on some meta information.
 * **path**:
   If `type: path`, the path that will be used to locate this type.
   Defaults to the type name with a `_` prepended. (so, for a content
   type named `talks`, the default path would be `_talks`)
 * **meta_key**:
   If `type: meta`, the meta key that will be used to locate this type.
   Defaults to `type`.
 * **meta**:
   If `type: meta`, the value of the meta key that will be used to
   locate this type. Defaults to the singularized name.
 * **publish_drafts**:
   Whether or not to publish drafts of this type. In the production
   environment this defaults to **false**. Otherwise, the default value
   is **true**.
 * **layout**:
   The default layout to use for this type. Defaults to the singularized
   name of the type.
 * **permalink**:
   The default permalink to use for this type.
 * **enabled**:
   Whether or not the content type should be enabled. Defaults to
   `true`.

---

## The Content Create Command

New in Sculpin 3.0, the `sculpin content:create` command will
automatically define the YML changes and create placeholder HTML and
Markdown assets for your specified content type.

### Usage

Running this command will create a new "**Projects**" content type with
boilerplate files as well as the taxonomy "**Tags**" for organizing the
project entries by custom tags.

    vendor/bin/sculpin content:create -b -t tags projects

This will output:

    Generating new content type: projects
    =============================================
    YAML to add to app/config/sculpin_kernel.yml:
    =============================================

    sculpin_content_types:
        projects:
            type: path
            path: _projects
            singular_name: project
            layout: project
            enabled: true
            permalink: projects/:title
            taxonomies:
                - tags

    =================END OF YAML=================


    Generating boilerplate for portfolio

> Don't forget to add the YAML to your `sculpin_kernel.yml` file.

The following boilerplate files and directories will be generated,
thanks to the `-b`/`--boilerplate` option:

    `-- source/
       |-- _projects/          - Folder that stores Projects
       |-- _views/
       |   `-- project.html    - Layout file for Projects
       |-- projects/
       |   |-- tags/
       |   |   `-- tag.html    - Listing template for individual "tags"
       |   `-- tags.html       - Main list for "tags" taxonomy
       `-- projects.html       - Template for the list of projects

All of these files are extremely bare-bones placeholders, meant to
provide a toehold for getting started with building your site and taking
advantage of Sculpin's features for aggregation (taxonomies) and
pagination.

Once you apply the YAML changes, you can create your first Project entry
and see how the defaults look:

*%PROJECT_DIR%/source/_projects/sculpin.md*

    ---
    layout: project
    title: Project SCULPIN
    tags: [blog, howto]
    ---
    Lorem ipsum dolor belta lowdah ...

> Run `vendor/bin/sculpin generate --watch --server` and browse to your
> sculpin site's projects folder (e.g.,
> `http://localhost:8000/projects`) to see your new Project entry.

Continue reading for an overview of how these files tie together to
deliver custom content.

---

## A Sample Content Type

The following is a sample content type called **projects**.

    sculpin_content_types:
        projects:

That's it! It wires everything up using defaults. Isn't magic fun?

### Configuration

The default values are expanded below. Please note that **you do not
have to specify all of these options**, this merely shows the
configuration options you *can* set, if you need to change the defaults.

    sculpin_content_types:
        projects:
            type: path
            path: _projects
            singular_name: project
            layout: project
            enabled: true
            taxonomies:
                - tags


### Data Providers and Generators

Given the above configuration, a few data providers and a generator will
be made available:

 * **projects** (data provider):
   This is created based on the name of the type. It contains a sorted
   list of all of the sources that are discovered for the content type.
    * **next_project**:
      Each item in the **projects** collection will have a
      **next_project** meta data that contains either **null** or the
      next project in the collection.
    * **previous_project**:
      Each item in the **projects** collection will have a
      **previous_project** meta data that contains either **null** or
      the previous project in the collection.
 * **projects_tags** (data provider):
   This is a `Sculpin\Contrib\Taxonomy\ProxySourceTaxonomyDataProvider`
   that contains a mapping from tags to projects.
 * **projects_tag_index** (generator):
   This is a `Sculpin\Contrib\Taxonomy\ProxySourceTaxonomyIndexGenerator`
   that will create a page for each tag.
    * **tag**:
      Each generated tag index will have a piece of meta data named
      **tag** that will contain the name of the tag for which the index
      is being generated.
    * **tag_projects**:
      Each generated tag index will have a piece of meta data named
      **tag_projects** that will be the collection of all projects with
      this tag.
 * **project.tag_html_index_permalinks** (source property):
   Each source (in this case, each project source) will have have a map
   of each taxon to its indexes for each type (html, json, xml) if any
   are available. If there is an HTML page that uses the
   `projects_tag_index` generator, then `tag_html_index_permalinks` will
   be added to each project source.

### Sample Projects Index Page

The following is a sample of a template that can be used to list all
projects.

    ---
    use: [projects]
    ---
    {% verbatim %}<ul>
        {% for project in data.projects %}
            <li><a href="{{ project.url }}">{{ project.title }}</a></li>
        {% endfor %}
    </ul>{% endverbatim %}

### Sample Project Tags Index Page

The following is a sample of a template that can be used to list all
tags that have been used to tag projects.

    ---
    use: [projects_tags]
    ---
    {% verbatim %}<ul>
        {% for tag,projects in data.projects_tags %}
            <li><a href="{{ site.url }}/projects/tags/{{ tag|url_encode(true) }}">{{ tag }}</a></li>
        {% endfor %}
    </ul>{% endverbatim %}

### Sample Project Tags Projects Index Page

The following is a sample of a template that leverages the tag index
generator to create a new page for every tag and list its projects.

    ---
    generator: projects_tag_index
    ---
    <h1>{{ page.tag }}</h1>
    {% verbatim %}<ul>
        {% for project in page.tag_projects %}
            <li><a href="{{ project.url }}">{{ project.title }}</a></li>
        {% endfor %}
    </ul>{% endverbatim %}

### Pagination of custom types

Custom types can be paginated in the same way as posts.

    ---
    generator: pagination
    pagination:
      provider: data.projects
    use:
      - projects
    ---
    <h1>Paginated Projects</h1>
    {% for project in page.pagination.items %}
      <li><a href="{{ project.url }}">{{ project.title }}</a></li>
    {% endfor %}

The `use` list will load all the items in each given provider into the
key data.{{provider_name}}. So, in this example, all the projects
available will be loaded into `data.projects`. By setting the provider
of pagination to `data.projects`, we are able to paginate our custom
type instead.
