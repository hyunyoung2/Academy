---
date: 2017-02-07
title: Introduction to blogging
video_id: erMOQmaMdVM
description: Write articles in Markdown and publish them as a blog
category: Blogging
tags:
  - jekyll-blogging
  - jekyll-layouts
resources:
  - name: Posts documentation
    link: https://jekyllrb.com/docs/posts/
  - name: Source code
    link: https://github.com/CloudCannon/bakery-store/tree/posts
type: Video
set: basics
set_order: 14
icon: blog
---
## Introduction

In this tutorial we'll create a few blog posts and list them on our [demo Bakery Store site](https://github.com/CloudCannon/bakery-store/tree/posts).

## Creating a post

Blog posts live in the `_posts` directory. Each post is stored in its own file. The file name of a post is important, the beginning has the date when the post was or will be published, then there's a title and finally an extension. By default, blog posts are commonly written in Markdown but can also be written in HTML. We'll create a new file for our first post: `_posts/2016-04-03-chocolate-chip-cookies.md`.

In our post we'll start with empty front matter. We need this empty front matter to tell Jekyll that this isn't a static file. Then we'll add our Markdown content:

{% raw %}
~~~html
---
---
The chocolate chip cookie was invented by Ruth Graves Wakefield. She owned the Toll House Inn, in Whitman, Massachusetts, a very popular restaurant that featured home cooking in the 1930s. Her cookbook, Toll House Tried and True Recipes, was first published in 1936 by M. Barrows &amp; Company, New York. The 1938 edition of the cookbook was the first to include the recipe "Toll House Chocolate Crunch Cookie" which rapidly became a favorite cookie in American homes.

Source / Read more [Wikipedia](https://en.wikipedia.org/wiki/Chocolate_chip_cookie)
~~~
{% endraw %}

We'll repeat this for another post, `_posts/2016-04-04-sourdough-bread.md`:

{% raw %}
~~~html
---
---
Sourdough bread is made by the fermentation of dough using naturally-occurring lactobacilli and yeast. Sourdough bread has a mildly sour taste not present in most breads made with baker's yeast and better inherent keeping qualities than other breads, due to the lactic acid produced by the lactobacilli.

Source / Read more [Wikipedia](https://en.wikipedia.org/wiki/Sourdough)
~~~
{% endraw %}

## List all posts

We have two blog posts on our site, let's have a page which lists all the posts. We'll create `blog.html` in the root of the site and add front matter to set the layout and title:

{% raw %}
~~~html
---
layout: page
title: Blog Page
---
~~~
{% endraw %}

Next we'll output the blog posts in an unordered list, each post will have a link and title. Jekyll gives us access to an array of all the posts at `site.posts`. A post object has special properties. `url` is the URL for the generated post page, `date` is (by default) the date specified in the file name and `title` is (by default) the title specified in the file name:

{% raw %}
~~~html
...
<ul>
  {% for post in site.posts %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
~~~
{% endraw %}

![Blog posts](/images/tutorials/blogging/blog-list.png){: .screenshot}

When we click on a post it takes us to the generated page:

![Blog post](/images/tutorials/blogging/post.png){: .screenshot}

## Post layout

The generated page currently has no styling because there's no layout. Let's create a layout at `_layouts/posts.html`, inherit the page layout then output the title, date and content. Jekyll automatically converts the markdown content into HTML:

{% raw %}
~~~html
---
layout: page
---

<h2 class="spacing">{{ page.title }}</h2>
<p>{{ page.date }}</p>

{{ content }}
~~~
{% endraw %}

Now we need to add the layout in `_posts/2016-04-03-chocolate-chip-cookies.md` and `_posts/2016-04-03-chocolate-chip-cookies.md`.

{% raw %}
~~~html
---
layout: posts
---
...
~~~
{% endraw %}

![Formatted blog post](/images/tutorials/blogging/formatted-post.png){: .screenshot}

## Date filter

That's almost there except the date is too long. We can run it through a [date filter](/jekyll/date-formatting/) to fix the formatting:

{% raw %}
~~~javascript
...
<p>{{ page.date | date: '%B %d, %Y' }}</p>
...
~~~
{% endraw %}

![Date](/images/tutorials/blogging/date.png){: .screenshot}
