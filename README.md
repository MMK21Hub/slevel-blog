# Slevel blog source code

This repository contains the source code for my personal blog at **[📖 blog.slevel.xyz](https://blog.slevel.xyz)**.

It uses Jekyll with the [Minima](https://github.com/jekyll/minima) theme. It's deployed by [Netlify](https://www.netlify.com/) (so <https://mmk21-blog.netlify.app> is an alternative domain).

## Development instructions

```bash
# Using sudo here is really stupid,
# but Bundler seems to insist on writing to root-owned directories
sudo bundle install
bundle exec jekyll serve
```
