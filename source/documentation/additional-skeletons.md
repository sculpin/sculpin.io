---
title: Additional Skeletons
slug: getstarted/skeletons
---
Skeletons are a great way to bootstrap a Sculpin website.

They are bare-bones examples that include initial Twig template files for
various parts of a Sculpin website, as well as some initial CSS/JS/Images to 
get started.

## Default Bootstrap Blog

Getting up and running with this Bootstrap-based blog is covered in the Sculpin [Get Started](/getstarted/) guide.  

## NEW: Tailwind Blog

This blog uses the Tailwind utility-based CSS framework. Utility-based CSS is a great way to get a site started up quickly with fully custom design elements. 

Getting things in place just the way you want them gives you the insight necessary to decide what deserves to be abstracted and what can live on as a one-off.

To get started with the Tailwind Blog, use this command:

```
composer create-project beryllium/sculpin-tailwind-blog-skeleton myblog
```

Once the main assets are installed, change into the directory and run:

```
yarn encore dev
```

Then, you can run this to start Sculpin and try out your new site:

```
vendor/bin/sculpin generate --watch --server
```

<span class="screenshot">
![Desktop Site](/assets/skeletons/2019-08-31-desktop-blog-screenshot.png)
</span>

<span class="screenshot mobile">
![Mobile Site](/assets/skeletons/2019-08-31-mobile-blog-screenshot.png)
</span>

If you want the webpack encore assets to regenerate in the background, e.g.,
when you are editing your CSS, JS, and images, run this command in a separate 
terminal:

```
yarn encore dev --watch
```

---

## NEW: Tailwind Product Site

Need to make a company website or a product landing page? This is the skeleton for you. It strips out all the stuff related to blogging and leaves you with just the pieces you need to tailor the exact experience you want to deliver.

To get started with the Tailwind Product Landing Page, use this command:

```
composer create-project beryllium/sculpin-tailwind-landing-skeleton myproduct
```

Once the main assets are installed, change into the directory and run:

```
yarn encore dev
```

Then, you can run this to start Sculpin and try out your new site:

```
vendor/bin/sculpin generate --watch --server
```

If you want the webpack encore assets to regenerate in the background, e.g., if
you are editing your CSS, JS, and images, you can run this command in a separate
terminal:

```
yarn encore dev --watch
```

<span class="screenshot">
![Desktop Landing Page](/assets/skeletons/2019-08-31-desktop-landing-screenshot.png)
</span>

<span class="screenshot mobile">
![Mobile Landing Page](/assets/skeletons/2019-08-31-mobile-landing-screenshot.png)
</span>
