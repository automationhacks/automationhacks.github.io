---
title: Migrated away from Wordpress
excerpt:
  "How i moved away from Wordpress and into the worlds of static site generators with Jekyll and
  Github pages"
layout: post
permalink: /2020/07/25/writing-clear-bug-reports/
image: /assets/images/wp-content/uploads/2020/07/undraw_bug_fixing_oc7a.png
categories:
  - Testing theory
---

Hello there,

For folks who have been following my **earlier** blog on `https://automationhacks.blog` site, quite
recently you might have started seeing that the site cannot be found, fret not.

I've recently moved the blog away from Wordpress and have dived into the wonderful word of static
site generators using Jekyll and Github pages

## Why

Wordpress had been great for me. It enabled me to start blogging without any consideration of the
technical setup needed and it was quite easy to have a fully featured blog within minutes

However over time, the experience felt a bit bloated with lot of friction in place. For any new
functionality that i might need I have to **add Wordpress plugins** (and that requires a business
plan at the least), Wordpress as a platform has good power and you can easily setup a business
site/blog very quickly.

It however conflicted with my goals of having a minimal, fast technical blog/portfolio site that I
have full control over and customize to whatever needs might arise and that motivated me to move
this blog away from Wordpress

## Going basic

I had been aware of static site generators (SSG) before and had heard of Jekyll, Hugo, Sphinx among
many others. I did not want to get locked into another platform like Ghost and that's when I decided
to take a plunge into the wonderful word of SSG

Jekyll is probably one of the best static site generators out there and has a very tight integration
with Github, plus the hosting of the site is **very graciously** taken care of by Github. I had to
only buy the domain on Namecheap and do setup and was good to go. 🙌

There were many good tutorials that other people had put out for this process and you can check it
out [Blog from samba_code](https://dev.to/samba_code/migrating-a-blog-from-wordpress-to-jekyll-4flk)
or from [Hadi Hariri](https://hadihariri.com/2013/12/24/migrating-from-wordpress-to-jekyll/)

however I will add some of the additional steps that i did after moving away

## Download content from Wordpress and import into Jekyll

- You can download Wordpress content and then import using some
  [Jekyll import tool](https://import.jekyllrb.com/)
- Once done with above you should have a site with all the posts in `_posts` directory

## Install ruby and gems

Jekyll docs are very well written and explain these in detail, Before starting ensure you have Ruby,
RubyGems and other libs setup. Follow instructions from
[Jekyll Quickstart](https://jekyllrb.com/docs/)

Below are the steps to create a new Jekyll site

Create an empty Jekyll site with default minima theme

```zsh
jekyll new <yourname.github.io>
```

Serve the newly created site on localhost, which you can access on port 4000.
[localhost:4000](http://localhost:4000/):

```zsh
bundle exec jekyll serve
```

In Jekyll, posts are maintained in `_posts` directory and are ordered in `yyyy-mm-dd-<title>`, You
can also write drafts in `_drafts` folder and Jekyll will not serve this on your site till you move
it under posts

If you wan to view drafts in your local served Jekyll website

```zsh
jekyll serve --draft
```

## Let's start customizing

Jekyll uses [`Gems`](https://rubygems.org/) for most of the additional functionality that you might
need and associated plugins, Below is the basic process for installing and adding any new Gem into
the site

Add below lines in `_config.yml` under `group :jekyll_plugins do`, these are the ones that I have
initially added 

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

Fixes to make

- Replace below patterns with character listed next:

```zsh
&#8217; '
&nbsp; <space>
```

- Find html code blocks with data-gist and replace with below liquid tag

```ruby
{% gist d366955370d58dc2ca40c185b62cd829 %}
```

- Search for `<figure> or <img>` tag and replace it with `![image alt text](path_to_assets)`
- Search for `<pre>` tag and replace with code-block in order to get syntax highlighting using
  jekyll rouge
- Replace `!&nbsp` with ``
- Replace `/assets/images/wp-content` to all image URLs beginning with `/wp-content`
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
