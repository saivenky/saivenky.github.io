---
layout: post
title: Obsidian and Git
tags:
  - raw
  - coding
created: 2023-01-22
---
I've been having some troubles with my new writing workflow. My goal is to:
* Use Obsidian to write content
* Use Git to manage versions and sync across devices
* *Use Jekyll / GitHub Pages to publish content (This part has not been an issue)*

## Problem
When I use `git diff`, I want short diffs of what changed. When you are changing written content, that often includes paragraphs of text, the format of the saved file is quite important.

### Option 1: Saving paragraphs as a single line of text
  * Bad for Git because it's hard to pinpoint what exactly changed. It appears as though an entire paragraph changed even if you just fixed one typo in one small section of the paragraph.
  * Good for Obsidian because "soft line breaks" appear as a line break in Editor mode, but are rendered correctly (i.e. removed) in Reading mode. Since saving a paragraph as a single line has no line breaks, that means both Editor and Reading modes will match up and you don't need to toggle between the two.

### Option 2: Reformatting paragraphs with soft line breaks
* Good for Git because now the problem mentioned earlier is mitigated. You have broken up the paragraph into small pieces with soft line breaks. This means that if you change a part of the paragraph, then only a small part of the paragraph is highlighted when you do `git diff`.
* Poor for Obsidian because although Reading mode is unaffected, Editor mode now has shows those soft line breaks. This is very distracted from actually writing content.

And that last point is the crux of the issue. I want good diffs, but I don't want to see soft line breaks in Editor mode because it's distracting. If I add some content to a paragraph, all of a sudden I end up with a incredibly long line with a bunch of shorter lines.

## Solution
Can we change the behavior of `git diff`? Can't we just make Git *try harder*? Probably. Although the entire line appears to have changed in Option 1, what if we ask it highlight specific word-level changes?

Apparently the solution to all my problems (see [documentation](https://git-scm.com/docs/git-diff#Documentation/git-diff.txt---word-diffltmodegt)):
```
git diff --word-diff
```

And to display word diffs for a particular commit:
```
git show <commit> --word-diff
```

Although this outputs the entire file instead of just lines that changes, this is okay. Editing written paragraphs of text looks very different from editing code.

In particular, I don't ever see myself change multiple files of written content. I would most likely edit one specific post and commit that. In editing code, you are much more likely to change multiple 100+ line files, and in those cases, display the entire contents of the file for `word-diff` would definitely be a problem.