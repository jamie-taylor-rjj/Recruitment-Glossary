---
title: "Technologies Used"
description: "A one page summary of how to get Recruitment Glossary up and running locally. This is required in order to add content to it."
lead: "A one page summary of how to get Recruitment Glossary up and running locally. This is required in order to add content to it."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
images: []
menu:
  docs:
    parent: "start-here"
weight: 130
toc: true
---

## Tech Stack

This project makes use of Hugo and npm

{{< details "Which packages?" >}}
Whilst Hugo is entirely self-contained, this project makes use of a few npm packages to give search, syntax highlighting, and linting.

For a full list of the packages used in this project, please see the [packages.json](https://github.com/jamie-taylor-rjj/Recruitment-Glossary/blob/main/package.json) file.
{{< /details >}}

## Hugo

[Hugo](https://gohugo.io/) is a static site generator which is built with the [Go programming language](https://go.dev/). It is one of the fastest static site generators (partly due to the speed of the Go programming language), but almost no knowledge of either Hugo or Go are required to use it.

Each page of this project is a markdown file, contains a number of very specific sections, and must exist within a certain location.

{{< picture img="/images/docs/start-here/technologies-used/file-location" alt="a screenshot of the Recruitment Glossary repository when loaded into Visual Studio Code. It shows that the content > en > docs > start-here directory is expanded, and the technologies-used.md file is selected in the file explorer. The majority of the image is taken up with the contents of the technologies-used.md file" caption="" >}}

All English language content should be stored within relevant directories under the `/content/en/docs` directory; whereas images should be stored in a relevant subdirectory under the `/static/images/docs` directory.

### Document Format

Each markdown document should have a very specific format. Each file should have TOML formatted front-matter (a section of code at the very top of the file, which describes the file). The following is the front-matter for this file:

```toml
---
title: "Technologies Used"
description: "A one page summary of how to get Recruitment Glossary up and running locally. This is required in order to add content to it."
lead: "A one page summary of how to get Recruitment Glossary up and running locally. This is required in order to add content to it."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
images: []
menu:
  docs:
    parent: "start-here"
weight: 130
toc: true
---
```

Under this should be the page content in markdown. Please see the [markdown for this page](https://github.com/jamie-taylor-rjj/Recruitment-Glossary/blob/main/adding-to-start-here/content/en/docs/start-here/technologies-used.md) for examples of how the content should be arranged.

### Shortcodes

Whilst Hugo is a fantastic static site generator, it is possible to extend it's capabilities by using shortcodes. These are short blocks of HTML which can be embedded into any content page, and this project has a number of useful shortcodes. All of the shortcodes for this repository can be found in the `/layouts/shortcodes/` directory.

### Picture

The picture shortcode is used to add an [HTML picture element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture) with a custom set of images. The picture element is the preferred way of displaying images over the `img` shortcode, as it allows the browser to pick the image which fits with its viewport and it has support for.

This shortcode has the following arguments:

- `img` is a path to an image to use
- `caption` is a caption to be displayed under the picture
- `alt` is alt text for users who have accessibility concerns

Of the above arguments, only the `img` one is required. The `img` argument is a path to the image file to display in the picture. One caveat is that you should provide three versions of the image to display:

- .jpg (full size)
- .webp (full size) &ast;
- -medium.jpg (a smaller version of the image)

{{< alert icon="💡" text="You can save images as webp using the [GNU Image Manipulation Program](https://www.gimp.org/)" />}}

The filename of the image to display should be provided _WITHOUT_ a file extension, too.

#### Example

For example, suppose you have a set of images in the `/images/docs/start-here/technologies-used/` directory called `file-location.jpg`, `file-location.webp`, and `file-location-medium.jpg`. Displaying them using the picture shortcode would require the following:

{{< code >}}
{{</* img="/images/docs/start-here/technologies-used/file-location" */>}}
{{< /code >}}

The above shortcode will render the following HTML:

{{< output >}}
<figure class="all-width">
    <picture>
        <source srcset="/images/docs/start-here/technologies-used/file-location.webp" type="image/webp" media="(min-width: 1200px)">
        <source srcset="/images/docs/start-here/technologies-used/file-location-large.jpg" media="(min-width: 1200px)">
        <source srcset="/images/docs/start-here/technologies-used/file-location-medium.jpg" media="(min-width: 800px)">
        <source srcset="/images/docs/start-here/technologies-used/file-location-medium.jpg" media="(min-width: 340px)">
        <img src="/images/docs/start-here/technologies-used/file-location-medium.jpg" class="img-fluid">
    </picture>
    <figcaption>
        <h5></h5>
    </figcaption>
</figure>
{{< /output >}}

## Other commands

Doks (the theme that Recruitment Glossary is based on) comes with commands for common tasks. [Commands →]({{< relref "build-commands" >}})
