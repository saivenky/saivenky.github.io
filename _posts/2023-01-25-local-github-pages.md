---
layout: post
title: Local GitHub Pages
tags:
  - raw
  - coding
created: 2023-01-25
---
If you're new to the Ruby ecosystem, testing GitHub Pages locally may feel a bit strange.

Steps are pretty simple though (assuming you don't run into hardware-specific issues like I did). I'm going to refer back to [this dependency versions page from GitHub Pages](https://pages.github.com/versions/).

1. Install `rbenv`: This is a tool that helps manage multiple Ruby versions.
2. `rbenv install 2.7.4`: You need Ruby 2.7.4 according to the dependencies (at the time of writing).
3. `rbenv local 2.7.4`: Running this within the Jekyll folder configures it so you use that specific version of Ruby when inside that folder.
4. Create a `Gemfile` with:
```
source 'https://rubygems.org'
gem "github-pages"
```
5. `bundle install`: Tells Ruby to install the gems listed in the Gemfile. It will also create a `Gemfile.lock` that is very explicit about all the packages and versions (including sub-dependencies) that were installed. One of these sub-dependencies should be `jekyll`, so there is no need specify that you need it.

    The only problem I ran into with the above step was that because I'm using an Mac with an ARM processor (i.e. M1 chip), some libraries needed to be built natively. This failed because I assume some compile dependencies for OpenSSL weren't found. Specifying them using the following command worked for me:
    ```
    PKG_CONFIG_PATH="$(brew --prefix openssl@1.1)/lib/pkgconfig" \
      gem install eventmachine -v '1.2.7'
    ```

6. `bundle exec jekyll serve`: Runs a local webserver with your content. The exact URL is printed in the terminal (usually `http://127.0.0.1:4000`). The `bundle exec` says to use the specific versions for this "bundle" (i.e. from the `Gemfile.lock`) rather than globally available versions.

If you'e never used `jekyll serve` before, it will also create a few files. This is the point of a static site generator. But to clean up those files after you're done testing, run `bundle exec jekyll clean`.

And that's it to test locally!
