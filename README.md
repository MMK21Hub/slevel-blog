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

## Deployment to Netlify instructions

- `RUBY_VERSION` environment variable should be set to `3.3.7`. Justification:
  - `bundler-2.6.0` requires Ruby `>= 3.1.0`
  - Jekyll tries to load `csv` from the standard library, which stopped being supported in Ruby `3.4.0` (see [2025-02-16-netlify.failed-build.txt](assets/2025-02-16-netlify.failed-build.txt) for log)
  - `3.3.x` is the latest major version that matches these requirements
  - `3.3.7` is the latest `3.3.x` version as of 2025-02-16
