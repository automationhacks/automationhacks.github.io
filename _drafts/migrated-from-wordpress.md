# Migrated from word press

Fixes to make

- Replace below patterns with character listed next:

```zsh
&#8217; '
```

- Find html code blocks with data-gist and replace with below liquid tag

```ruby
{% gist d366955370d58dc2ca40c185b62cd829 %}
```

- Search for `<figure> or <img>` tag and replace it with `![image alt text](path_to_assets)`
- Search for `<pre>` tag and replace with code-block in order to get syntax highlighting using jekyll rouge
- Replace `!&nbsp` with ``
- Replace `/assets/images/wp-content` to all image URLs beginning with `/wp-content`
- Update canonical_url in dev.to or medium.com if the blog was cross posted
- Finally check local site if all looks good at `http://127.0.0.1:4000/`

> There would be lot of HTML mixed with markdown in the blog and while you can certainly fix them into a markdown syntax, it would take a long time. I decided to let it be as long as the URLs were fine

## References

- [Migrating a blog from Wordpress to Jekyll](https://dev.to/samba_code/migrating-a-blog-from-wordpress-to-jekyll-4flk)
- [Jekyll docs](https://jekyllrb.com/docs/)
- [Setting up domains in Github pages](https://docs.github.com/en/github/working-with-github-pages/about-custom-domains-and-github-pages)
- [4 steps to migrate from Wordpress to Jekyll](https://blog.webjeda.com/wordpress-to-jekyll-migration/)
- [Migrating from WordPress.com to Jekyll](https://hadihariri.com/2013/12/24/migrating-from-wordpress-to-jekyll/)
