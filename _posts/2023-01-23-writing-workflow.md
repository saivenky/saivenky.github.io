---
layout: post
title: "Writing Workflow"
categories: dev
created: 2023-01-23
date: 2023-01-23
---
This is my writing workflow with Obsidian and GitHub Pages.

### Folder Structure
```
.
├── CNAME
├── _config.yaml
├── _drafts/
├── _posts/
├── about.md
├── index.md
└── preface.md
```

This root folder (i.e. what I labeled above as `.`) can now be:
* Repository root in GitHub
* Vault folder in Obsidian

### 1. Writing Content

Using Obsidian, I can now create content under `_drafts/` or in `_posts/`. Drafts is not published by default so you can just use this for private notes if you want. I have not decided exactly what I'm going to do with it yet, but for now, I've just imported a few "blog-like" notes that I had written using Notion.

Once I incubate and hatch some of those thoughts, they might end up in `_posts/`. This is where I will have all published content.

Either way, both of these can easily be edited using Obsidian.

### 2. Front Matter (i.e. metadata)

In Jekyll (the static site generator used by GitHub Pages), Front Matter is the little section at the top that holds metadata. This metadata is used for determining the page layout, title of the page, and other data should you choose to customize how your metadata is processed. Mine currently looks like:

```yaml
---
layout: post
title: "Writing Workflow"
tags:
  - raw
created: 2023-01-23
---
```

The cool thing is that Obsidian also processes the front matter for Tags. This means I get free tooling to easily navigate tags as I'm writing or searching my content.

### 3. Publishing

As mentioned before, all published posts are within the `_posts/` folder. Because I'm using GitHub pages, this means I also am using Git to manage this content. You can use Git's [word-diff]({% post_url 2023-01-22-discovering-git-word-diff %}) to view sane diffs of what changed.

For now, my commit history uses some structure. My commits start with:
* `post: <Title>` for the first publish of a post
* `edit: <Description of edit>` for edits to content after the first publication
* `meta: <Description of change to metadata>` for non-content (i.e. metadata) changes

Afterwards, just push the commit to GitHub and GitHub Pages takes over.

### 4. Editing

I want to treat posts as living, changing content. I'd like to treat it almost like documentation of topics or parts of my life. So I am currently freely changing published content. Git tracks it all, but I'm also tracking the last edited date via Front Matter like so:

```yaml
---
edited: 2023-01-23
---
```

The reason I'd like do this is to make a distinction between "raw" thoughts and ideas that I've iterated on a few times. To a reader, there should be a different in quality of the posts. The "raw" posts will appear more as "stream of consciousness", whereas the "edited" posts will have some structure.

Key observation is that posts, drafts, raw, and edited are a 2x2 matrix. It's possible to have edited drafts and raw posts.
