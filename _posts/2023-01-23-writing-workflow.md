---
layout: post
title: "Writing Workflow with Obsidian and GitHub Pages"
categories: dev
description: "A step‑by‑step look at how I draft, edit, and publish blog posts using Obsidian and GitHub Pages powered by Jekyll."
created: 2023-01-23
date: 2023-01-23
last_modified_at: 2025-04-28
tags:
  - writing
  - workflow
  - obsidian
  - git
  - github pages
  - jekyll
  - blogging
---
My writing workflow is purpose‑built for speed and clarity. Here's the exact writing workflow I use to turn raw notes in Obsidian into polished articles served by Jekyll on GitHub Pages.

## Why document the workflow?

Writing it down forces me to keep the system simple, and-bonus-it lets you steal any part that helps you ship faster.

## Why this stack?

* **Obsidian** keeps all content as plain Markdown so I can version it.
* **Jekyll** converts that Markdown into a fast static site.
* **GitHub Pages** hosts the result for free and runs the build on every push.

## Folder structure

```text
.
├── CNAME
├── _config.yml
├── _drafts/
├── _posts/
├── about.md
├── index.md
└── preface.md
```

Repo root = Obsidian vault = GitHub repository. One folder, zero friction.

## 1. Draft in Obsidian

- Draft ideas live in `_drafts/`- on publishing the site, Jekyll excludes them, so I'm free to brain‑dump.
- Once an idea "hatches," I rename the file to the `YYYY-MM-DD-slug.md` format and move it to `_posts/`.
- Obsidian's backlink graph helps me connect posts as they develop.

## 2. Add front matter early

Every markdown file opens with YAML so Jekyll can render it and my theme can surface metadata:

```yaml
---
layout: post
title: "How to Name Your Commits"
tags: [git, workflow] # for SEO
created: 2025‑04‑28 # if this started as a draft
date: 2025-04-28 # published date
last_modified_at: 2025‑04‑28 # for tracking freshness
---
```

Because Obsidian also processes the front matter for tags, you get free tooling to easily navigate tags while writing or searching content.

Tip: set **`last_modified_at`**-you'll thank yourself later.

## 3. Commit & push with Git

I treat commits as a changelog:

- `post: writing‑workflow` - first publish
- `edit: clarify folder tree` - content change
- `meta: update tags` - metadata only

Then: `git push origin main` and let GitHub Pages build.

> Need to view clean diffs? Try `git diff --word-diff` (I wrote about it [here]({% post_url 2023-01-22-discovering-git-word-diff %})).

## 4. Iterate publicly

Posts are living docs. I refine them when:

1. A reader points out a gap.
2. I learn something new.
3. I spot awkward phrasing while researching a later post.

Because front matter stores **`last_modified_at`**, readers know the post's freshness at a glance.

## Takeaways

- Keep the repo, vault,and site in one folder.
- Add metadata early-future‑you will thank you.
- Let Git history tell the story; your blog just needs the latest commit.
