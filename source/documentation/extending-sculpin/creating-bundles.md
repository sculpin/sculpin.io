---
title: Creating Bundles
slug: extending-sculpin/creating-bundles

---

To start creating bundles to extend Sculpin, check the Symfony 2 section on
[Bundles][1], especially the
[How to use Best Practices for Structuring Bundles][2] documentation. There
really is not much more to extending Sculpin that writing Symfony 2 bundles
that hook into [Sculpin's event lifecycle][3].

Register your own bundles as described in the [configuration][4] section.

You may find it helpful to look at the existing [community extensions][5]
for inspiration and examples.

[1]: http://symfony.com/doc/current/cookbook/bundles/
[2]: http://symfony.com/doc/current/cookbook/bundles/best_practices.html
[3]: {{site.url}}/documentation/extending-sculpin/lifecycle/
[4]: {{site.url}}/documentation/extending-sculpin/configuration/
[5]: {{site.url}}/documentation/extending-sculpin/community-extensions/
