# Jekyll Tutorial
This project is a product by following the [Jekyll tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/).

Some notes for each step.

## 1. [Setup](https://jekyllrb.com/docs/step-by-step/01-setup/)
It's best to go to the directory of your project and run `bundle init`, then you will have a `Gemfile` created in that directory. E.g. in Windows, using PowerShell, you may enter and see the following:

```PS
PS C:\your\project\path> bundle init
Writing new Gemfile to C:/your/project/path/Gemfile
```

After adding the line `gem "jekyll"` to your `Gemfile`, you would run `bundle` from the same place. E.g. this is what you may see on Windows:

```PS
PS C:\your\project\path> bundle
Fetching gem metadata from https://rubygems.org/............
Resolving dependencies...
Bundle complete! 1 Gemfile dependency, 32 gems now installed.
Use `bundle info [gemname]` to see where a bundled gem is installed.
```

## 2. [Liquid](https://jekyllrb.com/docs/step-by-step/02-liquid/)

If you don't add front matter to the top of the `index.html` file, you will see `{{ "Hello World!" | downcase }}` displayed on your site, not the intended `hello world!`.

## 3. [Layouts](https://jekyllrb.com/docs/step-by-step/04-layouts/)

It seems the `_layouts` directory is automatically recognized by jekyll. Other than adding that directory, nothing else is done and the `default.html` layout is recognized and applied to the pages.

## 4. [Includes](https://jekyllrb.com/docs/step-by-step/05-includes/)

The `_includes` directory is also automatically recognized by jekyll. After creating the `navigation.html` file and modifying the `default.html` file, the site looks like below:

![site_with_navigation](/screenshots/navigation.png)

## 5. [Assets](https://jekyllrb.com/docs/step-by-step/07-assets/)

Let me try to straight out the relationship here...

- The page `index.html` is wrapped around by a layout `default.html`, i.e. the contents of `index.html` are inserted into `default.html` as object `{{ content }}`, and the title is passed in as object `{{ page.title }}`.

- The layout `default.html` references the navigation settings in `navigation.html` by including it as a tag `{% include navigation.html %}` (specifically, an `include` tag).

- In `navigation.html`, items (page names and links) defined in `navigation.yml` are iterated by the `for` tag, page names and links are passed in as objects `{{ item.name }}` and `{{ item.link }}`. 

- For the styling in `navigation.html`, it is using a styling class `current` that is defined in `_sass/main.scss`.

- The styling class is made aware to the site builder by adding the line `<link rel="stylesheet" href="/assets/css/styles.css">` to layout `default.html`.

## 6. [Deployment](https://jekyllrb.com/docs/step-by-step/10-deployment/)

This note is important to me, because I'd likely use GitHub Pages.

> Note: if publishing your site with GitHub Pages, you can match production version of Jekyll by using the `github-pages` gem instead of `jekyll` in your `Gemfile`. In this scenario you may also want to exclude `Gemfile.lock` from your repository because GitHub Pages ignores that file.

After adding the tags for RSS feed and SEO meta tags (i.e. `{% feed_meta %}` and `{% seo %}`), you will not see the added information on the displayed pages. It will be added to the pages' source code instead.
