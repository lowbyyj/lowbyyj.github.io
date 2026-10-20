---
layout: default
title: Projects
permalink: /projects/
---

# Projects

Tools and systems I built, most of them because something kept getting in my way. Building the tool first, and fixing it myself when it breaks, has been a habit since I was a kid.

These days AI is part of the toolbox, so I can build more of them, faster. The habit hasn't changed.

## Tools I Built

### [Personal Voice Keyboard]({{ '/projects/personal-voice-keyboard/' | relative_url }})

A voice input tool for Windows and Android. Even when Korean and English are mixed in one sentence, it decides which terms to keep in their original language, tidies up the wording, and puts the result on the clipboard. Refined through daily use and judged by the total time spent waiting and correcting rather than raw latency, it now also learns misheard terms from my corrections.<br>
**Type:** Personal AI Tool / In Active Daily Use<br>
**Focus:** Korean-English mixed dictation, technical terminology preservation, learning from corrections, and API key isolation through a shared serverless proxy.

### [AI Gauge]({{ '/projects/ai-gauge/' | relative_url }})

<img src="{{ '/assets/projects/ai-gauge/widget-dual.png' | relative_url }}" alt="AI Gauge widget showing Codex as a fuel gauge and Claude as a tachometer (sample data)" style="float:right;width:260px;max-width:35%;height:auto;margin:0 0 1rem 1rem" loading="lazy">

An Android home-screen widget that shows my Codex and Claude usage at a glance: Codex as a fuel gauge for what's left, Claude as a tachometer for what's used, each with a pace marker that shows whether usage is running ahead of an even pace. It comes with a built-in reading guide drawn like an engineering blueprint, with numbered callouts that explain each needle and number.<br>
**Type:** Personal AI Tool / In Daily Use<br>
**Focus:** At-a-glance usage tracking, pace against the reset window, car-dial widget design, and a blueprint-style reading guide.

<div style="clear:both"></div>

### Text Washer

A brutally simple Android scratchpad: paste anything, get plain text back. On Windows, I'd always used Notepad to strip the formatting from copied text, but Android had nothing like it, so I made one. It does that one job and nothing else: no permissions, no network access, no account.<br>
**Type:** Android Utility / Public Release 1.0.4 ([GitHub](https://github.com/lowbyyj/ThatIsTextWasher) · [APK](https://github.com/lowbyyj/ThatIsTextWasher/releases/latest/download/Text-Washer.apk))<br>
**Focus:** Plain-text cleanup on Android, a single-purpose design, zero permissions, and no network access.

### Lighter for ChatGPT

A Chrome extension for very long ChatGPT conversations. Past a certain length, typing and scrolling started to lag. Rather than split the conversation and lose its context, I made the page lighter: older messages that are off-screen wait to render, while the latest messages, streaming replies and scroll-back work as usual.<br>
**Type:** Browser Extension / In Daily Use<br>
**Focus:** Typing and scrolling responsiveness, deferred rendering of off-screen messages, and keeping long conversations intact.

### Shopping via Telegram

A shopping workflow that runs through a Telegram chat with an AI agent. A message like "I'm out of bleach" is enough: the agent finds the one I usually buy and puts it in the cart. It could take the order all the way to my door, but it stops at checkout, so the last tap stays mine.<br>
**Type:** AI Agent Workflow / Personal Use<br>
**Focus:** Plain-language requests over Telegram, matching the products I usually buy, cart automation, and a human final step before payment.

---

## Behind the Tools

### [My AI Agent Harness]({{ '/projects/agent-harness/' | relative_url }})

Several AI models, each in the role I found it best at. Claude Opus talks through the work and the big picture with me. GPT-6.1 Sol implements from tightly written specs, since left to plan on its own it tends to over-engineer. Claude Sonnet steps in when Sol stalls, and GPT-6 Astra reviews high-stakes changes and reads fine detail in images. Around them sit one long-running session per project, a session that turns links I find into skills every other session can use, an assistant on my always-on home server, and the same live sessions on my PC and my phone.<br>
**Type:** Personal System / In Daily Use<br>
**Focus:** Role-based routing across models, spec-first delegation, high-stakes review, PC-to-phone continuity, and guardrails added only where something actually went wrong.

---

## Before the AI Era: Field-Tested Foundations

Field-tested foundations of how I build: seeing a real problem, building the missing system, and iterating until it works.

A lot of my engineering work starts the same way: I see a real-world bottleneck, sketch the system that could remove it, build the missing pieces, and keep fixing the messy parts until the system works.

### [Physical Systems and Wireless Measurement]({{ '/projects/field-tested-foundations/' | relative_url }})

Robotics, automated Wi-Fi CSI measurement, drone-based aerial connectivity experiments, and motorized antenna systems built to answer questions that clean models alone could not.

**Type:** Physical Systems / Wireless Measurement / Research Platforms<br>
**Focus:** robotics and embedded prototyping, automated antenna positioning, custom measurement tools, drone-mounted smartphones, RF experiment setup, motor control, shielding, and field-tested data collection.
