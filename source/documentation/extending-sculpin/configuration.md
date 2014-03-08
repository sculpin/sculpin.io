---
title: Configuration
slug: extending-sculpin/configuration

---

To configure Sculpin for additional bundles, a custom Sculpin kernel must be
created. Sculpin will automatically look for this file in
`app/SculpinKernel.php`. If this file exists, it it is loaded. If not, Sculpin
simply loads a default kernel.

If this file does not yet exist, you can use this template to create it:

    <?php

    class SculpinKernel extends \Sculpin\Bundle\SculpinBundle\HttpKernel\AbstractKernel
    {
        protected function getAdditionalSculpinBundles()
        {
            return array(
            );
        }
    }

In order to enable a Scupin bundle, just make sure that its class name is a part
of the array returned from `getAdditionalSculpinBundles`. For exmaple, to load
the [mavimo/sculpin-redirect-bundle][1], whose class is
`Mavimo\Sculpin\Bundle\RedirectBundle\SculpinRedirectBundle`, you would do
the following:

    <?php

    class SculpinKernel extends \Sculpin\Bundle\SculpinBundle\HttpKernel\AbstractKernel
    {
        protected function getAdditionalSculpinBundles()
        {
            return array(
                'Mavimo\Sculpin\Bundle\RedirectBundle\SculpinRedirectBundle'
            );
        }
    }

Please note that you must return the class name as a string! This is slightly
different from traditional Symony 2 usage.

That's it! This will ensure that your bundle will be registered correctly.

[1]: https://github.com/mavimo/sculpin-redirect-bundle
