---
layout: post
title: "Discovering Git Word Diff"
categories: dev
created: 2023-01-22
date: 2023-01-22
edited: 2023-01-28
---
When I use `git diff`, I want short diffs of what changed. When you are changing written content, that often includes paragraphs of text, the format of the saved file is quite important.

This has been hindering my new writing workflow. My tools of choice are:
* Use [Obsidian](https://obsidian.md/) to write content
* Use Git to manage versions and sync across devices
* Use Jekyll / GitHub Pages to publish content (This part has not been an issue)

### Option 1: Saving paragraphs as a single line of text

Let's use the intro paragraph as a demonstration:

```
When I use `git diff`, I want short diffs of what changed. When you are changing written content, that often includes paragraphs of text, the format of the saved file is quite important.
```

Bad for Git because it's hard to pinpoint what exactly changed. It appears as though an entire paragraph changed even if you just fixed one typo in one small section of the paragraph. For example, if I change the word "quite" to "very" at the end, then the diff is:

```diff
-When I use `git diff`, I want short diffs of what changed. When you are changing written content, that often includes paragraphs of text, the format of the saved file is quite important.
+When I use `git diff`, I want short diffs of what changed. When you are changing written content, that often includes paragraphs of text, the format of the saved file is very important.
```

However, this is good for Obsidian because "soft line breaks" appear as a line break in Editor mode, but are rendered correctly (i.e. removed) in Reading mode. Since saving a paragraph as a single line has no line breaks, that means both Editor and Reading modes will match up and you don't need to toggle between the two.

### Option 2: Reformatting paragraphs with soft line breaks

Let's use the same paragraph as before but include line breaks:

```
When I use `git diff`, I want short diffs of what
changed. When you are changing written content,
that often includes paragraphs of text, the format
of the saved file is quite important.
```

Good for Git because now the problem mentioned earlier is mitigated. You have broken up the paragraph into small pieces with soft line breaks. This means that if you change a part of the paragraph, then only a small part of the paragraph is highlighted when you do `git diff`.

Remove the word "quite", this time the diff is:

```diff
When I use `git diff`, I want short diffs of what
changed. When you are changing written content,
that often includes paragraphs of text, the format
-of the saved file is quite important.
+of the saved file is very important.
```

However, this is poor for Obsidian because although Reading mode is unaffected, Editor mode now has shows those soft line breaks. This is very distracted from actually writing content.

And that last point is the crux of the issue. I want good diffs, but I don't want to see soft line breaks in Editor mode because it's distracting. Instead of focusing on what I'm writing, I keep thinking about the jagged line lengths.

### Solution

Can we change the behavior of `git diff`? Can't we just make Git *try harder*? Although the entire line appears to have changed in Option 1, what if we ask it highlight specific word-level changes?

The solution to all these problems is using `word-diff` (see [documentation](https://git-scm.com/docs/git-diff#Documentation/git-diff.txt---word-diffltmodegt)):

```shell
# Diff of current changes
git diff --word-diff
# Diff of a particular commit
git show <commit> --word-diff
```

Now we can format full paragraphs in a single line, and the diff of our previous change is:

```diff
When I use `git diff`, I want short diffs of what changed. When you are changing written content, that often includes paragraphs of text, the format of the saved file is [-quite-]{+very+} important.
```

If you scroll to the right in the code block above, you now see:
* `[-quite-]` for the block that was deleted and
* `{+very+}` for the block that was added.

Much easier to pinpoint the change this way. In my terminal, those are highlighted in red and green respectively, so it's even easier to spot.
