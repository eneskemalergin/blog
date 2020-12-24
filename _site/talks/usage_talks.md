# talks
Here is a separated repository for adding presentation page into jekyll blog powered with jekyll and reveal js

Here with this repository I powered my website with the presentations and talks that I gave. All presentations are viewable directly on the web.


Presentations are just "posts" as Jekyll calls them.  Each presentation is just a file in the `_posts` directory.  You can create a presentation really easily with Brenns's setup:


```
---
title: Example
layout: presentation
description: This is an example presentation.
---
{{ site.startslide }}
# Example

This is my example presentation.  I'm using markdown to write it.
* Bullet points are simple.
* [Links](/index.html) are concise.

> Blockquotes are effortless

    print('Syntax highlighting is easy!')
{{ site.endslide }}
```

Front Matter
------------

In the front matter, you have to set `layout: presentation`, as well as your
presentation's title and a description.  The description is used in the talk
listing.  You can additionally specify:

- `theme`: use any theme name in Reveal's [theme list][].  Only use the name,
  not the `.css` ending, or any filepath.  The default is `theme: solarized`.
- `highlight`: choose the syntax highlighting theme.  Choose from any of
  Highlight.js's syntax highlighting [themes][syntax] (anything under the
  "styles" directory).  Just use the name, no `.min.css` or anything else.  The
  default is `highlight: zenburn`.
- `remotes`: Set this to any value you'd like (`true` is a good choice) to allow
  the Remotes.io plugin, which lets you use a smartphone as a presentation
  remote by scanning a QR code.  Default is disabled.


Slides
------

To write your slides, you can use the following variables which expand into
HTML:

* `site.startslide` - mark the beginning of a slide
* `site.endslide` - mark the end of a slide
* `site.nextslide` - a short cut for `{{ site.endslide }}{{ site.startslide }}`.
* `site.startvertical` - start a vertical slide group
* `site.endvertical` - end a vertical slide group

They're a bit janky, but they get the job done.  I don't have too much support
"built-in" yet for more advanced usage of Reveal.js; I'll add it if I need it.

All of your content can be written in Markdown.  It's actually converted to HTML
by Javascript, not by Jekyll.  So keep in mind that each slide is essentially a
snippet of Markdown.  There are probably idiosyncracies that will result.  You
can do syntax highlighting using the normal triple-backtick notation of
Markdown.

You can do LaTeX by employing the double-dollar sign `$$\int_a^b f(x)
\:\mathrm{d}x$$` syntax that's normal with MathJax.  Not all of LaTeX is
perfectly supported under MathJax, so it's worth doing some previewing with
Jekyll before deploying!

[theme list]: https://github.com/hakimel/reveal.js/tree/master/css/theme
[syntax]: https://cdnjs.com/libraries/highlight.js
