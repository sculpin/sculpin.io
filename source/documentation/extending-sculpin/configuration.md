---
title: Configuration
slug: extending-sculpin/configuration

---

## Additional bundles

To configure Sculpin for additional bundles, a custom Sculpin kernel must be
created. Sculpin will automatically look for this file in
`app/SculpinKernel.php`. If this file exists, it is loaded. If not, Sculpin
loads a default kernel.

If this file does not yet exist, you can use this template to create it:

    <?php

    class SculpinKernel extends \Sculpin\Bundle\SculpinBundle\HttpKernel\AbstractKernel
    {
        protected function getAdditionalSculpinBundles(): array
        {
            return [
            ];
        }
    }

In order to enable a Sculpin bundle, add its class name to the array returned
from `getAdditionalSculpinBundles`. For example, to load the
[mavimo/sculpin-redirect-bundle][1], whose class is
`Mavimo\Sculpin\Bundle\RedirectBundle\SculpinRedirectBundle`, you would do
the following:

    <?php

    use Mavimo\Sculpin\Bundle\RedirectBundle\SculpinRedirectBundle;
    use Sculpin\Bundle\SculpinBundle\HttpKernel\AbstractKernel;

    class SculpinKernel extends AbstractKernel
    {
        protected function getAdditionalSculpinBundles(): array
        {
            return [
                SculpinRedirectBundle::class,
            ];
        }
    }

Please note that you must return the class name as a string value! Do not
return and instance, and also do not return a hashmap like in Symfony 4.

That's it! This will ensure that your bundle will be registered correctly.

[1]: https://github.com/mavimo/sculpin-redirect-bundle

## Additional services

You can register services without bundles by creating a file `app/config/sculpin_services.yml`. 
Sculpin will register automatically all services declared or imported in that file.

For instance, you can register an existing Twig extension with the following file :

```yml
services:
  twig.extension.intl:
    class: 'Twig\Extra\Intl\IntlExtension'
    tags:
      - twig.extension
``` 

