---
layout: post
title:  "Feedback‑Loop Fat‑Loss: Using a 5‑Day Moving‑Average to Stay Lean and Strong"
created: 2025-05-02
date: 2025-05-08
categories: [strength]
tags: [fat‑loss, moving‑average, obsidian, dataviewjs, parent‑life]
excerpt: How a 5‑day moving average and a simple step‑count algorithm keep my cut on track—without sacrificing barbell numbers or toddler‑chasing energy.
---

## My Scale vs. My Toddler’s Cheerios

It’s 6 a.m. and I can hear my toddler giddily running through the hallways. Before he notices I'm awake and demands my attention, I tip-toe onto the scale and watch the number flash, and—just like yesterday—wonder if I should celebrate or panic.

Instead of letting one data point hijack my mood (and my calorie budget), I open my Obsidian daily note. There, a tiny line of code refreshes a **5‑day moving average (MA)** that tells me—calmly, mathematically—whether the ship is still on course. This simple metric is the backbone of my current cut: daily feedback, tiny course‑corrections, zero drama, and **no compromise on strength**.

## Why a Moving‑Average Beats Daily Scale Drama

* **Water & glycogen noise:** Hard leg day? Salty ramen? Either can swing the scale by a pound overnight.
* **Five days = sweet spot:** Three felt jumpy; seven lagged behind reality. Five smooths bumps yet reacts inside a week.
* **Decision‑ready metric:** The MA isn’t just a prettier graph—it’s the trigger for action (or restraint), exactly like a trailing stop‑loss in trading.

_Fewer “I blew it!” spirals; tighter alignment between what I **feel** and what’s actually happening under the skin._

## My Setup

* **Any Bluetooth scale** that syncs to Apple Health or Google Fit works. (Mine’s a $29.99 no‑brand special.)
* **Health → CSV → Obsidian:** I use *Health‑Auto‑Export* on macOS, but any pipeline that drops a simple CSV into your vault is fine.
* **DataviewJS block** inside my daily note calculates today’s 5‑day MA and renders it inline.

```dataviewjs
/* 5‑Day Moving‑Average code
   ↓ Paste your final block here once folder names & keys are set. */
````

<aside markdown="1">
**Why Obsidian?** Local files, instant back‑linking to training logs, and nerd‑level automation with zero SaaS bloat.
</aside>

## The Decision Engine (Daily)

| Status       | Threshold (Δ = today’s MA − yesterday’s MA) | Action                                                                                                              |
| ------------ | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Behind**   | **Δ < ‑0.10 lb**                            | + 500 steps NEAT (baseline = 5 k; cap = 12 k).<br>After 12 k, add 20 min LISS, **+ 5 min** each *extra* behind day. |
| **On‑track** | **‑0.10 ≤ Δ ≤ ‑0.20 lb**                    | Hold current NEAT/LISS.                                                                                             |
| **Ahead**    | **Δ < ‑0.20 lb**                            | ‑ 500 steps or ‑ 5 min LISS per day until you’re back at baseline (5 k steps, 0 min LISS).                          |

A single glance at the MA tells me whether to lace up for a stroller detour, tack on a treadmill session, or—my favorite—**do nothing** and lift like normal.

## 5 · NEAT & LISS Menu — Parent‑Proof Ways to Add (or Subtract) Calories

| + 500 Steps (\~25–35 kcal)                                               | + 5 min LISS (\~40 kcal)                            |
| ------------------------------------------------------------------------ | --------------------------------------------------- |
| **Stroller detour:** Park at the far end and loop once around the block. | **Incline treadmill:** 12 % grade, 3 mph.           |
| **Laundry lunges:** One lunge per shirt as you fold.                     | **Stationary bike:** Zone 2 pace, Netflix chunk.    |
| **Walking Pomodoro:** 2‑min lap every 25‑min work block.                 | **Row‑erg cruise:** Strokes < 24 spm, HR < 140 bpm. |

*These are **muscle‑neutral** additions—low‑impact, low‑cortisol, and easy to taper back when you’re “ahead.”*

## Muscle‑Retention Guardrails

1. **Protein ≥ 1 g/lb lean body mass.**
2. **Barbell compounds stay heavy:** ≥ 80 % 1RM twice weekly keeps fast‑twitch fibers honest <sup>(Schoenfeld et al., 2021)</sup>.
3. **Sleep triage:** blackout curtains + 20‑min afternoon nap if toddler tyranny strikes.
4. **Deload, don’t delete:** drop one set per lift when recovery tanks—do *not* slash intensity.

These guardrails let the scale drift south while squat and press numbers cling stubbornly north.

---

I’ll publish a follow‑up in **June** with DEXA numbers and a side‑by‑side “before/after MA chart,” so subscribe if you want to see the real‑world payoff.

---

### Next Reads

- `What to read next`
