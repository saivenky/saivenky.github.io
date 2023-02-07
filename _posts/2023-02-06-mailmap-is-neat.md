---
layout: post
title: "Mailmap Is Neat"
tags:
  - coding
created: 2023-02-06
published: 2023-02-06
---
I initially found mailmap in order to rewrite some Git history, but then realized it has use beyond one-time history rewrites. If you're creative, you can use it within enterprise too.

Git's official documentation is concise, so please read that too: https://git-scm.com/docs/gitmailmap

Essentially, let's say your git history has commits with the wrong email address. This can be accidental or intentional. For example, on my laptop, if I forget to configure my Git user and email, my commits have an author of `Sai <sai@Laptop.local>` (or something similar).

You can quickly amend this if this is the top commit:

```
git commit --amend --author="Sai <sai@realemail>" --no-edit
```

Otherwise it gets a bit tricker but still possible if you add in `git rebase`:

```
git rebase -i HEAD~3
# mark the commit in question with "edit"
# use the git commit --amend line from before
git rebase --continue
```

Now what if you work at a company and you accidentally pushed a commit with the wrong email. If you have branch protection (which your company should if it doesn't), then that means it's a permanent part of your company's history. But suppose we want to at least make the commit history *look* nice, even if in reality it isn't. Enter `mailmap`.

If I create a `.mailmap` file with the following contents:

```
Sai Tries Git <sai@realemail> Sai <sai@Laptop.local>
```

Then every occurrence of `Sai <sai@Laptop.local>` will be shown as `Sai Tries Git <sai@realemail>` in the commit history.

Excellent.

Now suppose we introduce a mailmap file into your repo. Now we can really get creative and start fixing bad emails, or perhaps even creating mappings to company emails instead of private emails, etc. You could even consider tying your "name" the same as your Slack handle and use it to map usernames across two systems. Of course this would be a manual process, but it only needs to happen once per user.

This acts like a layer abstracting away all the badness so `git log` and all history looks nice and neat. And as with all abstraction layers, the possibilities are endless!
