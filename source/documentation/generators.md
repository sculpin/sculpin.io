---
title: Generators
slug: generators

---

Generators are used to fabricate new virtual sources based on an existing
concrete source.

A good example of this would be tags or categories for posts. One would not want
to create a tag or category index page for every tag that may ever be created. A
generator can be used to create a tag or category index page dynamically based
on meta data from posts.

Another example would be pagination. If a list of posts needs to be paginated,
one would not want to create an index page for page 1 and page 2 and page 3. One
would prefer to have those pages generated automatically.

Sculpin ships with a Pagination generator.

---

## Pagination

The pagination generator allows you to create multiple pages around a set of
items. This is particularly useful if you want to create pages for a list of
collection of sources like you can get from a data provider.

### Kernel Configuration

 * **sculpin_pagination.max_per_page**:
   The default maximum number of items to show per page. This value can be
   overridden on a source-by-source basis. Default value is **10**.

### Source Level Meta Configuraton

 * **pagination.max_per_page**: The maximum number of items to show per page.
   Default value is set by the `sculpin_pagination.max_per_page` kernel
   configuration.

 * **pagination.provider**:
   The descriptor for the provider of the items to be paginated. The default
   value is `page.posts`.

    * **page.{key}**:
      Reference page meta data. This will allow a source to define its own simple
      collection of data that may be paginated.

    * **data.{key}**:
      Reference data provider data. The page must use the provider.

### Usage

    ---
    generator: pagination
    pagination:
        max_per_page: 3
    use:
        - posts
    ---
    {% verbatim %}<ul>
        {% for item in page.pagination.items %}
            <li><a href="{{ item.url }}">{{ item.title }}</a></li>
        {% endfor %}
    </ul>{% endverbatim %}

    <nav>
    {% verbatim %}{% if page.pagination.previous_page or page.pagination.next_page %}
        {% if page.pagination.previous_page %}
            <a href="{{ site.url }}{{ page.pagination.previous_page.url }}">Newer Items</a>
        {% endif %}
        {% if page.pagination.next_page %}
            <a href="{{ site.url }}{{ page.pagination.next_page.url }}">Older Items</a>
        {% endif %}
    {% endif %}{% endverbatim %}
    </nav>
