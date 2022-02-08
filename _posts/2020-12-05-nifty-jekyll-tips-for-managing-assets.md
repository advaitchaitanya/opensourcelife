---
layout: post
tags: code
title: Nifty Jekyll Tips for Managing Assets
---

<p class="drop-cap">We love Jekyll and the simplicity it offers. In case you're wondering, this site is powered by it and hosted on GitHub. Here's a few things we've found helpful.</p>

## Use Sass and Compress the Output

Because Jekyll give us built-in support for Sass, we can leverage that to compress our CSS. It's easy to setup.
1. Create a directory called `_sass` in the root of your project. This is where you'll store all your partials in.
2. Create another directory (we use the name `assets`) in your site's source folder. This'll house any entry file to import your partials.
3. Create a Sass file such as `styles.scss` inside the `assets` folder and start the file with two lines of triple dashes:

{% highlight sass %}
---
---

@import 'partial';

.my-definition {
  display: flex;
}
{% endhighlight %}

Your directory structure should look something like this:
```
|-- _sass
|    `-- _partial.scss
|-- assets
    `-- styles.scss
```

To enable compression, specify `compressed` as the output style in your `_config.yml` file:
```
sass:
  style: compressed
```

## Group Identical CSS Media Query Rules

If your partials share identical media query rules, you can create a Sass mixin to pack them together. This is what the PostCSS plugin [CSS MQPacker](https://github.com/hail2u/node-css-mqpacker) accomplishes. Dominique Briggs wrote an [article on Medium](https://medium.com/front-end-developers/the-solution-to-media-queries-in-sass-5493ebe16844) detailing how to accomplish this with Sass. Here's the basic concept.

Create a `_breakpoints.scss` file where all your media query definitions are stored.
{% highlight sass %}
@media (min-width: $breakpoint-md) { }

@media (min-width: $breakpoint-lg) { }
{% endhighlight %}

Create a responsive mixin for your components.
{% highlight sass %}
.component {
  font-size: 1rem;
}

@mixin component-md {
  .component {
    font-size: 2rem;
  }
}

@mixin component-lg {
  .component {
    font-size: 4rem;
  }
}
{% endhighlight %}

Call the mixins in your `_breakpoints.scss` file.
{% highlight sass %}
@media (min-width: $breakpoint-md) {
  @include component-md;
}

@media (min-width: $breakpoint-lg) {
  @include component-lg;
}
{% endhighlight %}

## Integrate Autoprefixer

> Autoprefixer is PostCSS plugin to parse CSS and add vendor prefixes to CSS rules using values from Can I Use.

Vincent Wochnik created a plugin that adds support for Jekyll. It's straightforward to incorporate.

Install the gem.
```
$ gem install jekyll-autoprefixer
```
Add the following lines to your `_config.yml` file:
```
plugins:
- jekyll-autoprefixer
```

Read more about configuring it on the [Jekyll Autoprefixer GitHub repository](https://github.com/vwochnik/jekyll-autoprefixer). One thing to note: GitHub pages only allows a [set of whitelisted plugins](https://pages.github.com/versions/).

## Cache Bust CSS and JS Files

You can add a unique timestamp to your styles and scripts URL for each build. This is a useful way to ensure your visitors get the latest version of your assets. We accomplish this by appending a query string using the `site.time` variable:

{% raw %}
```
<link href="/assets/styles.css?{{ site.time | date: '%s' }}" rel="stylesheet">
```
{% endraw %}

This is a simple solution if your assets are small. But, it's important to recognize that for every visit, browsers will have to download them anew.

## Compress HTML

Fortunately, Anatol Broder created a [Jekyll layout](http://jch.penibelst.de) to accomplish this with the [Liquid template language](https://shopify.github.io/liquid/). That means we don't have to install any plugins; it'll be GitHub Pages compatible.

1. Download the latest release from the [GitHub repository](https://github.com/penibelst/jekyll-compress-html).
2. Extract the `compress.html` file and copy it to your `_layouts` directory.
3. Reference the `compress` layout in your highest-level layout, which is typically `_layouts/default.html`.

{% raw %}
```
---
layout: compress
---

<!DOCTYPE html>
<html lang="en">
  <title></title>
  <meta content="width=device-width, initial-scale=1.0" name="viewport">
  <body>
    {{ content }}
  </body>
</html>
```
{% endraw %}
