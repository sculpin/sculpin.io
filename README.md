Sculpin Website
===============

This repository contains (almost) everything that makes up
[sculpin.io](http://sculpin.io).

Powered by [Sculpin](https://github.com/sculpin/sculpin). =)

&copy; Dragonfly Development Inc.


Build
-----

    composer install
    ./vendor/bin/sculpin generate --watch --server

Your newly generated clone of [sculpin.io](https://sculpin.io) is now
accessible at `http://localhost:8000/`.

Submit & Publish
----------------

The recommended process for submitting a PR to the site is to first
commit your changes to a branch on your fork, and then run the command
`composer publish` to update the `docs/` folder that is used for GitHub
hosting.  Commit the changes to `docs/` to the same branch, and then
submit the PR using the normal GitHub flow.

It's not mandatory to follow this recommendation, but it does help make
it easier on maintainers. They'll be able to click the "Merge" button
and the changes will be deployed immediately.

Notes
-----

* To add an item to the Documentation sidebar, modify the YAML in
  `app/config/sculpin_site.yml` to add the entry.