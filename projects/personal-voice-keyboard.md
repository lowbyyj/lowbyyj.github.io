---
layout: default
title: Personal Voice Keyboard
description: A private AI dictation system for Windows and Android.
permalink: /projects/personal-voice-keyboard/
---

# Personal Voice Keyboard

*A private AI dictation system for Windows and Android.*

Personal Voice Keyboard is a voice input tool I built for Windows and Android and use every day. Even when Korean and English are mixed in one sentence, it decides which terms to keep in their original language, tidies up the wording, and puts the result on the clipboard, ready to paste anywhere. It also keeps learning from the corrections I make.

## Why I Built It

Typing long messages to LLMs is tedious. I wanted real conversations with them, not slow finger-typed exchanges.

ChatGPT-style voice input was useful, but it stayed inside one app. I wanted to speak, get clean text, and paste it into whatever I was already using. I also needed Korean-first dictation that keeps intentional English terms, model names and shell commands intact. The real problem was never just speech recognition; it was turning speech into reliable, paste-ready technical text.

## How It Works

I press a key or tap a tile, speak, and stop. The audio goes to a small serverless proxy, gets transcribed and cleaned up, and comes back as text on the clipboard.

```text
Windows / Android app
        |  audio + app token
        v
Cloudflare Worker proxy   (API key, model choice, cleanup rules, glossary)
        |
        v
OpenAI transcription  ->  GPT-based cleanup
        |
        v
clean text  ->  clipboard
```

The apps know only the proxy address and an app token. The API key, model choice, cleanup rules and a terminology glossary all live in the proxy, so both apps improve together whenever the proxy does, without a rebuild.

The cleanup follows a simple rule: keep the meaning and the intentional English terms, drop meaningless fillers, and never summarize or invent. Models are picked by blind comparisons on my own speech, weighing quality against latency and cost, and a newer model is an option rather than an automatic upgrade.

## What's New (October 2026)

**Fix it where you read it.** Both apps now have a Review screen. I edit the result, the corrected text goes straight back to the clipboard, and the proxy learns misheard terms and punctuation habits from the difference. Rather than scoring edits with fixed rules, it reads the whole before and after, and each reply says exactly what was learned.

## Windows and Android

On Windows, PVK lives in the system tray. One hotkey handles both recording and sending, and a slim bar appears only while it is listening or processing, with an estimated finish time while it works.

Daily use turned up one real problem: long recordings could come back incomplete even when every request had succeeded. Long takes are now transcribed in overlapping chunks and stitched together before a single cleanup pass, and the latest recording stays on disk, so a failed run can be retried instead of spoken again.

On Android, a Quick Settings tile opens a small capture panel over whatever app I'm using, so I can keep scrolling and tapping underneath while I talk. The app shares the Windows look and has a Korean interface, and a failed recording is never lost: I can retry it or discard it.

## Security and Privacy

For now, PVK is a tool I use myself, not a public service, and its source is private. I may release it someday. The OpenAI key never goes into the apps. It stays on the proxy, and the apps only know how to reach it.

## Development Workflow

I make the product calls: what it should do, how it should feel, what counts as safe, and which model is worth the cost. Daily use decides the next patch. It is also one of the projects I run on [my AI agent harness]({{ '/projects/agent-harness/' | relative_url }}).

## What I Learned

- The number that mattered was total time, waiting plus fixing, not raw model speed.
- A glossary in the cleanup step fixed most terminology problems without turning on expensive search for everything.
- Daily use was a better guide than any feature plan.

## Status and What's Next

In daily use on Windows and Android, and still changing as I use it. Possible next steps: a Play Store release with a proper privacy policy and simpler onboarding, a glossary editor, and a search fallback for names it isn't sure about.

## Personal Note

I want to leave a small note to myself here: congratulations on finishing this one. Finished, that is, until tomorrow's use turns up the next thing to fix.

This project began with a very practical frustration. Even typing a message to an LLM often felt like friction, especially on a phone. I wanted to talk to LLMs more like I think: freely, at length, with corrections handled after the thought was spoken rather than before it was written.

The clipboard-first design became the key. The tool does not immediately send my words into one specific app. It turns speech into cleaned text, puts it on the clipboard, and lets me decide where it goes. That small detail changed the feeling of the whole workflow.

Ironically, this started because I was impressed by ChatGPT-style voice input. After building this, I often prefer my own tool: I can speak for a long time, preserve technical terms, review the cleaned result, edit if needed, and paste it anywhere. It feels less like “dictation” and more like giving my thoughts directly to the computer.
