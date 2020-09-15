---
title: Migrated away from Wordpress
excerpt:
  "How i moved away from Wordpress and into the worlds of static site generators with Jekyll and
  Github pages"
layout: post
permalink: /2020/09/20/migrated-away-from-wordpress/
image: /assets/images/wp-content/uploads/2020/07/undraw_bug_fixing_oc7a.png
categories:
  - Programming
---

Hello there, friend 😄

I've recently moved the blog away from Wordpress and have dived into the wonderful word of static
site generators using Jekyll and Github pages. This post talks about how the process looked like and
what were some of the additional customizations I did. Let's get started.

## Why

Why the migration? You might ask, Wordpress had been great for me initially. It enabled me to start
blogging without any consideration of the technical setup needed and it was quite easy to have a
fully featured blog within minutes

However over time, the overall experience felt a bit bloated and what i realized is that I do not
really make use of all the capability that Wordpress as platform offered.

Also, For any new functionality that I might need, I had to **add Wordpress plugins** (and that
requires a business plan at the least)

It conflicted with my goals of having a minimal, fast technical blog/portfolio site that I have full
control over and customize to whatever needs might arise and this ultimately motivated me to take
the plunge and move away from Wordpress

## Welcome to the world of static site generators (SSG)

I had been aware of static site generators before and had heard of **Jekyll, Hugo, Sphinx** among
many others. Watched a few videos around this and ultimately found Jekyll to have the required
functionality and customization for my needs

One of the motivating factors in favor of Jekyll was that it has a very tight integration with
Github, plus the hosting of the site is **very graciously** taken care of by Github. I had to only
buy the domain on Namecheap and do setup and the site was good to go. 🙌

The icing on the top was that my entire workflow involves writing posts in plain markdown and then
using Git and Github for the publishing workflow. Can't get more minimal than that. 😆

There were many good tutorials that other people had **already** put out for this process and that i
referred while migrating, check them out

- [Tomomi Imura - How-to: Migrating Blog from WordPress to Jekyll, and Host on Github](https://girliemac.com/blog/2013/12/27/wordpress-to-jekyll/)
- [Sam Atkinson - Migrating a blog from Wordpress to Jekyll](https://dev.to/samba_code/migrating-a-blog-from-wordpress-to-jekyll-4flk)
- [Hadi Hariri - Migrating from WordPress.com to Jekyll](https://hadihariri.com/2013/12/24/migrating-from-wordpress-to-jekyll/)
- [WebJeda - 4 Steps To Migrate From WordPress To Jekyll](https://blog.webjeda.com/wordpress-to-jekyll-migration/)

Below are the steps that I took and my experience around it.

## Download content from Wordpress and import into Jekyll

Depending on which platform your current blog is hosted on, there are different importers that you
could use to convert the dumps to a format that Jekyll can understand

My site was hosted on `wordpress.com` and so I had to download the content and then run
[Jekyll import tool](https://import.jekyllrb.com/)

Once done with above, It gave me a sample layout with all the images and other posts in `_posts`
directory

## Install ruby and gems

Jekyll docs are very well written and explain these in detail, Before starting ensure you have Ruby,
RubyGems and other libs setup. Follow instructions from
[Jekyll Quickstart](https://jekyllrb.com/docs/)

Once done, Below are the steps to create a new Jekyll site

Create an empty Jekyll site with default minima theme

```zsh
jekyll new <yourname.github.io>
```

You can serve the newly created site on localhost, which you can access on port 4000.
[localhost:4000](http://localhost:4000/):

```zsh
bundle exec jekyll serve
```

In Jekyll, posts are maintained in `_posts` directory and are ordered in `yyyy-mm-dd-<title>`
format, You can also write drafts in `_drafts` folder and Jekyll is smart enough to not serve these
on your site until you are ready and move it under posts

If you want to view drafts in your local served Jekyll website

```zsh
jekyll serve --draft
```

## Let's start customizing with plugins

Jekyll uses [`Gems`](https://rubygems.org/) for most of the additional functionality that you might
need and associated plugins, Below is the basic process for installing and adding any new Gem into
the site

Add below lines in `_config.yml` under `group :jekyll_plugins do`, Below are the ones that I have
initially added and few of which I would explain in further sections or future blog posts

```ruby
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-seo-tag", "~> 2.6"
  gem "jekyll-gist"
  gem "jekyll-archives"
end
```

You can then install all the gems mentioned in `Gemfile` using below:

```zsh
bundle install
```

Then, add these under plugins list in `_config.yml`

```yml
plugins:
  - jekyll-feed
  - jekyll-paginate
  - jekyll-seo-tag
  - jekyll-gist
  - jekyll-twitter-plugin
  - jekyll-archives
```

## Manual fixes to be made

The export and import process leaves some cleanup activities to be done on the posts/pages

### Encoded Strings

- You might see some encoded strings show up and might want to replace with character listed next:

```zsh
&#8217; <single quote>
&nbsp; <space>
```

### Get Github gists to render

- Also if you've been using Github gists for code samples, You might find these not rendered on the
  page. To fix these, Find the html code blocks with data-gist and replace with below liquid tag,
  The cool thing here is that since its your own Github account, you only need to specify the UUID
  like ID for gists to be rendered

```ruby
{% gist d366955370d58dc2ca40c185b62cd829 %}
```

### Fix images

- Search for `<figure> or <img>` tag and replace it with `![image alt text](path_to_assets)`, You might have all the images in a `wp-content` folder and so the easiest thing is to move the entire folder under `assets/images` and then fix the references to these images
- To be more specific, replace all image URLs beginning with `/wp-content` with `/assets/images/wp-content`

### Optional updates

- Search for `<pre>` tag and replace with code-block in order to get syntax highlighting using
  Jekyll rouge
- Update canonical_url in dev.to or medium.com if the blog was cross posted
- Finally check local site if all looks good at `http://127.0.0.1:4000/`

> There would be lot of HTML mixed with markdown in the blog and while you can certainly fix them
> into a markdown syntax, it would take a long time. I decided to let it be as long as the URLs were
> fine

## References

- [Jekyll docs](https://jekyllrb.com/docs/)
- [Setting up domains in Github pages](https://docs.github.com/en/github/working-with-github-pages/about-custom-domains-and-github-pages)
- [4 steps to migrate from Wordpress to Jekyll](https://blog.webjeda.com/wordpress-to-jekyll-migration/)
- [Migrating from WordPress.com to Jekyll](https://hadihariri.com/2013/12/24/migrating-from-wordpress-to-jekyll/)

To learn more about Jekyll, Check out
[Mike danes videos on YouTube](https://www.youtube.com/watch?v=T1itpPvFWHI&list=PLLAZ4kZ9dFpOPV5C5Ay0pHaa0RJFhcmcB)

https://desiredpersona.com/google-analytics-jekyll/
https://desiredpersona.com/disqus-comments-jekyll/

## Categories and posts and getting an archive

Jekyll documentation on [Categories](https://jekyllrb.com/docs/posts/#categories) and can use
[Jekyll archives plugin](https://github.com/jekyll/jekyll-archives) to display post archives
