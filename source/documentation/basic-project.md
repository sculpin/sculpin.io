---
title: Basic Project
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
    `-- sculpin.json                   # Dependencies

To generate a Sculpin site, you must have at least the directory `source` (although it can be an empty directory).