---
layout: post
title: "Dad‑Bod Debugging: 5‑Day MA Fat‑Loss Plan in Obsidian"
categories: [strength]
created: 2025-05-02
date: 2025-05-08
excerpt: "Log weight in Obsidian, use a 5‑day MA trendline, and a step dial to melt dad‑bod fat without sacrificing muscle—or toddler playtime."
tags: [fat‑loss, moving‑average, obsidian, dataviewjs, step‑count, parent‑life, neat]
---

## 6 a.m. Scale Jitters vs. a Bowl of Oatmeal 🥣

The kid is already sprint‑crawling for breakfast. I sneak onto the scale, watch the number flash, and decide—*nope, not letting that one datapoint hijack my mood*.

In Obsidian, a **5‑Day Moving Average (MA)** updates itself and tells me, in plain English: _“still on course—keep breakfast the same.”_ That little graph is my invisible coach: zero drama, zero guesswork, zero sacrifice in the gym.

## Why You Should Trust a Moving‑Average, Not Your Scale

* **Water & glycogen whiplash:** Long lower‑body session? Salty ramen? Either can swing the scale by a pound overnight.
* **Five‑day ≈ Goldilocks window:** Three felt twitchy; seven lagged. Five keeps you honest within a work‑week.
* **It’s your trading stop‑loss:** When the MA drifts outside target, you adjust *once*—no over‑corrections.


## Zero‑Code Setup (Copy‑Paste Friendly)

* **Any bodyweight scale** → Nothing fancy needed.
* **Obsidian daily note** → Manually jot a `weight:` field in your Daily note.
* **This DataviewJS snippet** calculates the MA.

_Copy-paste this into a new note (I call mine `Weight Tracker.md`)._
```js
// truncated for blog readability; full gist linked below
const days = dv
  .pages('"Daily"')
  .where(p => typeof p.weight === 'number')
  .sort(p => p.file.name, 'desc');
/* ...compute 5‑day MA, delta, table render... */
```

_Full code? [Grab the gist](https://gist.github.com/saivenky/b2ad55e5eb917bb2a80578c3d2d76ad1)_


## The Decision Engine — One‑Look Fat‑Loss Dials

| Status      | Δ (today MA – yesterday MA) | **What I Change**               |
| ----------- | --------------------------- | ------------------------------- |
| **Slow**    | 0.00 → –0.09 lb            | +500 steps (cap 12 k, then add cardio)        |
| **On‑Plan** | –0.10 → –0.20 lb            | Hold steady                   |
| **Fast**    | < –0.21 lb                  | –500 steps (or –5 min cardio) |

No mental math. The MA tells me to *walk a bit more*, *walk a bit less*, or *leave it*.


## NEAT & LISS Menu — Friction‑Free Calorie Tweaks

| + 500 Steps                                                      | + 5 min Cardio                             |
| ---------------------------------------------------------------- | ------------------------------------------ |
| **Stroller detour**: park at the far end & loop the block once.  | **Incline treadmill**: 12 % @ 3 mph.       |
| **Walking Pomodoro**: 2‑min lap every 25‑min work block.         | **Stationary bike**: Zone 2, Netflix on.   |
| **Grocery‑lot gambit**: return the cart to the far corral—twice. | **Elliptical glide**: conversational pace. |

All picks are toddler‑friendly, joint‑kind, and easy to dial down when the MA says “chill.”


## Muscle‑Retention Guardrails

1. **Protein ≥ 1 g/lb lean body mass**—high‑protein diets spare muscle in a deficit <sup>(Phillips & Van Loon 2011)</sup>
2. **Compound lifts stay heavy**: keep machine or free‑weight compounds at ≈ 80 % of your normal load twice a week—heavy loads best protect strength <sup>(Schoenfeld et al. 2021)</sup>
3. **Sleep triage**: blackout curtains + a 20‑min power‑nap when *toddler takeover* wrecks the night.
4. **Deload, don’t delete**: drop one set—not the weight—if recovery tanks.

These rules let body‑fat trend south while weight‑stack numbers crawl north.


## Why Obsidian Over a Fancy App?

* **Local & portable**: markdown files live forever.
* **Back‑links**: click weight trend → last leg‑day notes → see what changed.
* **Automation**: DataviewJS means no subscription, no API limits.

_**Disclaimer**: I’m a data‑driven dad, not your doctor. Talk to a pro before making big nutrition or training changes._

### Next Reads

*I’ll share the first DEXA + MA chart combo in **June 2025**. You might enjoy these other posts in the meantime.*

* **[Upper‑Lower Split: 45‑Minute Strength for Busy Parents]({% post_url 2025-04-27-upper-lower-split-for-busy-parents %})** — the program behind these guardrails.
* **[From Interest to Identity: When Repetition Becomes “Who I Am”]({% post_url 2025-05-05-from-interest-to-identity%})** — how tiny data points hard‑wire habits.
* **[Writing Workflow with Obsidian + GitHub Pages]({% post_url 2023-01-23-writing-workflow %})** — the pipeline that makes this post auto‑update itself.
