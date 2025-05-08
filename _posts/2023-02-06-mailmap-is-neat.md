---
layout: post
title: "Clean Up Your Git History with .mailmap"
category: dev
date: 2023-02-06
last_modified_at: 2025-04-28
tags:
  - git
  - mailmap
excerpt: Learn how to use Git's built-in `.mailmap` file to fix wrong author names and email addresses and keep your contributors list tidy.
redirect_from: /2023/02/06/mailmap-is-neat
---
## Why .mailmap?

Ever found your Git log peppered with variations of **you**-work laptop here, personal desktop there, maybe an ancient email you don't even own?

A `.mailmap` file tells Git:

* "Whenever you see *this* author/email, show it as *that* instead."
* No history rewrite, no force-push, no drama.

Result? A spotless `git log` when viewing contributors and commit history.

## Quick fix for **one** dangling commit

If the **top** commit is the only offender:

```bash
git commit --amend --author="Sai <sai@real.email>" --no-edit
```

Done.

## When the mistake is **already pushed**

History is immutable on a protected branch-but **appearance** isn't.

Create a file named `.mailmap` at the repo root:

```text
Sai Tries Git <sai@real.email>  Sai <sai@Laptop.local>
```

Now every `git log`, `git shortlog -sne`, and GitHub "Contributors" widget will show the canonical identity.

Need to verify?

```bash
git check-mailmap "Sai <sai@Laptop.local>"
# -> Sai Tries Git <sai@real.email>
```

## Enterprise-scale tricks

| Use-case | `.mailmap` pattern |
| --- | --- |
| Map to corporate email from personal email | `Sai <sai@corp.com> <sai@home.dev>` |
| Consolidate many machines | `Sai <sai@corp.com> sai <laptop@local>`<br/>`Sai <sai@corp.com> Sai Tries Gaming <sai@gaming>` |
| Slack handles for automating pinging authors | `@sai <sai@real.email> Sai <sai@real.email>` |

The file supports _names_, _emails_, or **both**. Blank lines and `# comments` are ignored.

## Gotchas & tips

* **File location** - `.mailmap` at repo root, or configure a path via `git config mailmap.file "path/to/file"`.
* **No SHA change** - because commits stay untouched, your collaborators don't need to re-clone.
* **Keep it in source control** so future contributors inherit the mapping.

## Next steps

* Read the concise [official docs](https://git-scm.com/docs/gitmailmap).
* Pair this with `git shortlog -sne` for a one-liner **contributors report**.
* Want more small dev wins? Browse the **[Dev category](/dev)**.
