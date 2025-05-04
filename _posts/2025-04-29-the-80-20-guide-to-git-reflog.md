---
layout: post
title: "The 80/20 Guide to Git's 'Reflog'-Undo Anything Without Fear"
category: dev
created: 2025-04-29
date: 2025-05-01
excerpt: A practical, story-driven crash-course on `git reflog`. Learn the handful of commands that rescue 80% of real-world mistakes in under a minute.
tags: [git, dev-tools, productivity]
---
Last Monday while cleaning up some old branches, I pruned a feature branch that I was working on and **and nuked a week's worth of work**.
The fix took *fifteen seconds*-not because I'm a wizard, but because I finally grok **`git reflog`**.

If you've ever typed `git reset --hard` or deleted a branch and then gone _Oh \*\*\*\*_, this guide is for you.

To keep it focused: I'm covering the **few reflog moves that cover 80% of everyday disasters**, plus a copy-paste alias so future-you can recover even faster.

## What **is** the reflog (30s version)

- Git stores every change of `HEAD` (and each branch) in a rolling log-**the reflog**.
- Entries live for 90 days by default (`git config --get gc.reflogExpire`).
- The reflog is *local*; it doesn't travel with your pushes or pulls.

That's all you need to know to start rescuing things. The rest of this post shows you when and how.

## The 5 Most Common "Oh-No" Moments the Reflog Fixes 📋

1. **Accidental hard reset**: you ran `git reset --hard` and lost unpushed commits.
2. **Deleted branch**: `git branch -D feature-xyz`-and then realised it had work in progress.
3. **Force push gone wrong**: you rewrote history on `main` and want the pre-push state.
4. **Rebase headache**: an interactive rebase went sideways and `HEAD` sits on the wrong commit.
5. **Detached HEAD edits**: you checked out a commit, made changes, and now HEAD floats in space.

If any of these sound familiar, keep reading. We'll fix each with one short snippet.

## TL;DR Cheat-Sheet ("gundo" Alias)

Add this to your `.gitconfig`:

```ini
[alias]
  gundo = "!f(){ \
    git reflog --pretty='%C(yellow)%h%Creset %Cgreen%gd%Creset %s' -n $1; \
  }; f"
```

Usage:

```bash
git gundo           # show last 30 HEAD movements
git gundo 5         # show last 5 (faster)
```

Copy-paste now; thank yourself later.

## Scenario 1 - Recover After `git reset --hard`

```bash
# Step 1: See where HEAD *was* before the reset
git gundo 3
# 9a84e2d HEAD@{0} reset: moving to 9a84e2d
# 741fcb8 HEAD@{1} commit: add login form   ← we want this

# Step 2: Jump back
git reset --hard 741fcb8
```

🎉 You're back on the last good commit. Push (or re-push) as needed.

## Scenario 2 - Revive a Deleted Branch

You deleted `feature-linter`, but the work isn't on any remote.

```bash
git gundo | grep feature-linter
# fb0d211 HEAD@{7} checkout: moving from feature-linter to main

git checkout -b feature-linter fb0d211
```

The branch-and your work-are alive again.

## Scenario 3 - Undo a Bad Force Push

1. Note the hash *before* the push:

   ```bash
   git gundo 6 | grep push
   # 2c6d8a0 HEAD@{2} push: force-with-lease
   # 1a57b48 HEAD@{3} commit: big refactor ← safe state
   ```

2. Reset and push:

   ```bash
   git reset --hard 1a57b48
   git push --force-with-lease
   ```

Remote teammates breathe easy.

## Scenario 4 - Abort a Messy Rebase

During an interactive rebase you realise everything is tangled:

```bash
git rebase --abort            # bail out
git gundo 4                   # find HEAD before rebase
git reset --hard <good-hash>  # or checkout, if you prefer
```

## Scenario 5 - Save Work from a Detached HEAD

```bash
git commit -am "temp changes"
git gundo 4                   # spot the commit hash
git branch rescue-work <hash> # or merge it elsewhere
```

## Keeping the Log Around Longer

For long-lived side projects or rare-but-critical rollbacks:

```bash
git config --global gc.reflogExpire 180.days
```

Now entries linger six months before garbage collection.


## Reflog vs. Other Undo Tools

| Tool                | Best for | Caveat |
|---------------------|----------|--------|
| `git reflog`        | Any local history change | Local only |
| `git stash`         | Quick WIP snapshots | Easy to forget stashes |
| `git reset --soft`  | Move HEAD, keep index | Doesn't help after `--hard` |
| `git restore`       | Undo file changes | Newer Git (2.23+) |

_Reflog is the safety net underneath all the others._

## Building the Habit

1. **Alias first** - add `gundo` today; muscle memory beats Google search.
2. **Run `git gundo` *before* you panic** - it's often the fastest way to orient yourself.
3. **Share the rescue** - next time you help a teammate, link them here (or show them your alias file).

### Next Reads

* [My Site Got Hijacked → How I Recovered in an Hour]({% post_url 2025-04-23-my-site-got-hijacked %})
* [Upper-Lower Split: A 45-Minute Strength Routine for Busy Parents]({% post_url 2025-04-27-upper-lower-split-for-busy-parents %})) - redeem that saved coding time in the gym.
