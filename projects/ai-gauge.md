---
layout: default
title: AI Gauge
description: An Android home-screen widget that shows Codex as a fuel gauge and Claude as a tachometer.
permalink: /projects/ai-gauge/
---

# AI Gauge

<img src="{{ '/assets/projects/ai-gauge/widget-dual.png' | relative_url }}" alt="AI Gauge widget showing Codex as a fuel gauge and Claude as a tachometer (sample data)" style="display:block;width:100%;max-width:560px;height:auto;margin:1rem auto" loading="lazy">

AI Gauge is an Android home-screen widget that shows my AI coding allowances at a glance. Codex reads like a fuel gauge, showing what's left. Claude reads like a tachometer, showing what's used.

## Why I Built It

I kept opening the usage page to see how much of my Codex allowance was left before the next reset. I wanted to read it the way I read a fuel gauge, without opening anything. When I started using Claude as well, it got a second dial.

## How to Read It

Each dial has two needles: the long one follows the five-hour window, the short one the weekly limit. A thin outer ring ends in a dot that marks an even pace, so I can tell at a glance whether I'm running ahead of it or behind.

Under each dial, a big number shows what's left or used in the five-hour window, with three small lines below it: when it runs out at this pace, when the window resets, and the weekly figure.

The phone asks each service directly, about every 30 minutes, with no server in between.

## Design Calls

<img src="{{ '/assets/projects/ai-gauge/guide-p1.png' | relative_url }}" alt="AI Gauge help page drawn like an engineering blueprint, with numbered callouts" style="float:right;width:220px;max-width:35%;height:auto;margin:0 0 1rem 1rem" loading="lazy">

Codex tells you how much of your allowance is left, while Claude tells you how much you've used. That difference suggested a dashboard: what's left reads naturally as a fuel gauge, from Empty to Full, and what's used reads as a tachometer, from 0 to 100 with a redline near the top. I picked that car-dial direction out of four mockups and added a pace ring, so each needle also tells me whether I'm running ahead of an even pace or behind it.

The help page carries the same idea. Instead of a plain list of instructions, it is drawn like an engineering blueprint, with numbered callouts at right angles pointing to each needle and number, so learning the widget feels like reading the drawing of a real instrument.

<div style="clear:both"></div>

## Status

v0.8.0, running on my own phone. Sideloaded, with a private repo, and not on any store.
