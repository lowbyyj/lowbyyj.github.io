---
layout: default
title: My AI Agent Harness
description: The multi-agent setup I work in every day, and the rules I run it by.
permalink: /projects/agent-harness/
---

# My AI Agent Harness

This is the setup I work in every day. It isn't a product. It's a way of working that I designed, gave rules to, and keep adjusting as I use it.

```text
Me — direction, taste, final calls
  -> Claude Opus — talks through the work and the big picture
       -> GPT-6.1 Sol — implements from tight specs
       -> Claude Sonnet — steps in when Sol stalls
       -> GPT-6 Astra — reviews high-stakes changes
  + one long-running session per project
  + a knowledge vault every session can draw on
  + an assistant on my home server
```

## The Rules I Run It By

- Specs come tight. Agents spend their effort on exactly what I asked for, not on redesigns nobody asked for.
- Reversible changes go in first and get reviewed in parallel. Only the ones that are hard to undo wait for a review.
- An agent reports only what it actually checked. "It's fixed" means it saw the fix work, not that the build went through.
- Every project keeps its own long-running session, so contexts never get mixed up. When work passes from one project to another, it travels as a written handoff note instead of relying on anyone's memory.

## Ember: One Conversation on PC and Phone

I work at my PC, then pick up my phone and head out or step away, and the same session keeps going in my hand. When I come back and sit down, the PC shows exactly where I left off. That was the idea. In practice, Claude's desktop app didn't reconnect reopened sessions to the phone, so every reboot cut them off. It's a Claude-only problem, and you only hit it when you orchestrate many long-running sessions at once. Codex never had it. Ember is a small Windows tray app I built to fix that: when the PC starts, it wakes a "boot manager" session that reopens every project session and reconnects each one to my phone.

I set the experience first, along with two rules: no wake-up messages in my work chats, and no prep before I leave the desk. Then one question reshaped the design: why run every 30 minutes if it only matters at boot? That led to a session that wakes itself when it starts.

After everything passed, I had my own system reviewed for over-engineering. Two clever mechanisms were switched off, and it got simpler and more reliable. The next morning a surprise app update restarted everything mid-work, and a few minutes later all eight sessions were back on my phone without me touching anything.

## Guardrails

I add a guardrail only where something actually went wrong, like a guard against risky deletes or a rule that agents can't read each other's chat records. When agents spent too long waiting for my approval, I logged the prompts, found the bottleneck, and cut most of the waiting with one line of guidance.

## Small Tools Around It

A few small things make the setup pleasant to live with: a one-line usage meter above the input box in the Claude desktop app, notification sounds I synthesized myself (a two-note "ding-dong" when an agent needs me, a three-note music box when it's done), and an always-on home server, so I can start a new session from my phone even when my PC is off.

## Status

My daily setup since October 2026, and it keeps changing as I use it.

## Personal Note

The part I enjoy most is the casting: figuring out what each model is genuinely good at and building the team around that. The other is watching them talk to each other. When I actually read their exchanges, they greet each other politely and pass files back and forth.
