---
date: 2017-02-06
title: Gems, Gemfiles and the Bundler
video_id: zdJln6RBg8A
description: Overview of the Ruby ecosystem
category: Setup
tags:
  - jekyll-setup
  - jekyll-plugins
resources:
  - name: Source code
    link: https://github.com/CloudCannon/bakery-store/tree/ruby-eco
type: Video
set: intermediate
set_order: 6
---
## Introduction

The terms Gem, Gemfile and the Bundler are often used in the Ruby community. So what exactly do they mean and how do we use them?

## What is a Gem?

A Gem is a bundle of code we can include in Ruby projects. This allows us to take someone else's code and drop it into our own project. Gems can perform functionality such as:

* Converting a Ruby object to JSON
* Pagination
* Interact with APIs such as Github

Jekyll itself is a [Gem](https://rubygems.org/gems/jekyll) as well many Jekyll plugins including [jekyll-feed](https://github.com/jekyll/jekyll-feed), [jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag) and [jekyll-archives](https://github.com/jekyll/jekyll-archives).

## What is a Gemfile?

A Gemfile is Ruby's dependency management system or in other words, a list of Gems a Ruby project needs to run. We use Gemfiles on Jekyll sites when we have Jekyll plugins.

## What does a Gemfile look like?

Let's create a Gemfile for a Jekyll site using the jekyll-feed and jekyll-seo-tag plugins.

A Gemfile requires at least one source which tells us where to download the Gems. Unless we have an advanced use case [rubygems.org](https://rubygems.org) will be fine.

Next we specify the Gems we're using. We can include a version number if want a specific version. It's important to always include Jekyll in our Gemfile.

Usually we'd have to also specify our plugin Gems in `_config.yml` so Jekyll knows about them. We can avoid this by putting our plugin Gems in a "jekyll_plugins" group which Jekyll includes automatically.

{% raw %}
~~~ruby
source 'https://rubygems.org'

gem 'jekyll', '3.1.6'

group :jekyll_plugins do
  gem 'jekyll-feed'
  gem 'jekyll-seo-tag'
end
~~~
{% endraw %}

## What is the bundler and how do we use it?

The bundler is the program which reads the Gemfile and downloads the Gems. We can install the bundler by running:

{% raw %}
~~~bash
gem install bundler
~~~
{% endraw %}

When we create or change a Gemfile, we need to run `bundle install` which performs two tasks:

1. Creates a `Gemfile.lock` file if it doesn't exist. This file is auto-generated and includes all the Gems in `Gemfile` with the addition of a version number even if it wasn't specified. This ensures that other people we share the source code to will have the same version of the gems.
2. Downloads the gems in `Gemfile.lock`.

Usually when we run jekyll we'd do something like this:

{% raw %}
~~~bash
jekyll serve
~~~
{% endraw %}

When we're using a Gemfile we need to run Jekyll slightly differently. We might have multiple versions of the jekyll-feed plugin on our machine and if we run `jekyll serve`, it might use the wrong version. We can solve this using `bundle exec` which makes only the Gems in the Gemfile available. For example if we want to run `jekyll serve` we'd run:

{% raw %}
~~~bash
bundle exec jekyll serve
~~~
{% endraw %}

Using Gemfiles and the bundler makes dealing with different versions of plugins much easier and ensures we can have a consistent environment for our site across multiple machines.
