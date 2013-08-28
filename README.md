Sculpin Website
===============

This repository contains (almost) everything that makes up
[sculpin.io](http://sculpin.io).

Powered by [Sculpin](https://github.com/sculpin/sculpin). =)

&copy; Dragonfly Development Inc.


Build
-----

### If You Already Have Sculpin

    sculpin install
    sculpin generate --watch --server

Your newly generated clone of [sculpin.io](https://sculpin.io) is now
accessible at `http://localhost:8000/`.

### If You Need Sculpin

***Security Notice:*** *Never run anything you haven't personally reviewed
first. This `curl url | php` command should be done with care.*

    curl -sS -O https://download.sculpin.io/sculpin.phar
    php sculpin.phar install
    php sculpin.phar generate --watch --server
