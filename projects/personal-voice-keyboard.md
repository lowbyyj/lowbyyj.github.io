---
layout: default
title: Personal Voice Keyboard
description: A private AI dictation system for Windows and Android.
permalink: /projects/personal-voice-keyboard/
---

# Personal Voice Keyboard

*A private AI dictation system for Windows and Android.*

**Personal Voice Keyboard** is a private AI dictation system built for Windows and Android. It records short speech, routes the audio through a serverless proxy, transcribes it with OpenAI, cleans the result into paste-ready text, and copies it to the clipboard.

The project focuses on Korean-English mixed dictation, technical terminology preservation, low-friction mobile UX, and secure API key isolation. The core productivity gain is not only transcription, but speech-to-clean-text conversion: speak naturally, receive cleaned text, and paste it anywhere.

## Overview

The main workflow is intentionally simple:

```text
Speak -> Stop -> Transcribe -> Clean up -> Clipboard -> Paste
```

The system is designed as a completed personal tool rather than a public product or open-source release. It is currently used as a private workflow for faster, cleaner communication with LLMs and other writing surfaces.

## Why I Built It

Typing long messages to LLMs is tedious. I wanted to have real conversations with LLMs, not slow finger-typed exchanges.

ChatGPT-style voice input was useful, but it remained tied to a specific app or interface. I wanted a clipboard-first workflow that worked across tools:

```text
Speak -> get cleaned text -> paste anywhere
```

I also needed Korean-first dictation that could preserve intentional English terms, model names, shell commands, and technical phrases. For my use case, the important problem was not only speech recognition. It was turning speech into reliable, paste-ready technical text.

## User Experience

On Windows, the tool behaves like a lightweight keyboard-side utility:

```text
Tray app -> Ctrl+F11 start -> Ctrl+F10 stop/send -> Clipboard
```

On Android, the primary flow is designed around the Quick Settings tile:

```text
Quick Settings tile -> Compact capture -> Stop & Send -> Copied -> Return
```

The goal is to minimize context switching. I can start recording, stop when finished, wait for processing, and paste the result into whichever app or conversation I was already using.

## System Architecture

```text
Windows Client / Android App
        |
        | audio file + app token
        v
Cloudflare Worker Proxy
        |
        | protected OpenAI API key
        v
OpenAI transcription
        |
        v
GPT-based cleanup
        |
        v
clean_text -> clipboard
```

The architecture keeps the OpenAI API key out of the Windows and Android clients. Clients only know the proxy URL and an app token. The Cloudflare Worker proxy centralizes model selection, cleanup policy, glossary handling, and safety boundaries.

This was an important design choice because both clients can improve when the proxy prompt, glossary, or model policy is updated. A server-side terminology glossary helps preserve technical terms such as `sudo`, `systemctl`, `journalctl`, Jetpack Compose, and Cloudflare Workers.

Web search is off by default to control cost and latency. It may be explored later only as a fallback for uncertain proper nouns or emerging terms. Exact internal prompts and deployment details remain private.

## Model and Prompt Policy

The model policy prioritizes accuracy over raw speed. The cleanup step is designed to preserve meaning, avoid summarization, remove meaningless fillers, and produce text that is ready to paste.

The cleanup policy follows several constraints:

- Preserve the user's meaning.
- Do not summarize.
- Do not invent details.
- Remove meaningless fillers.
- Preserve intentional English technical terms.
- Correct misrecognitions only when context strongly supports the correction.
- Avoid overcorrection.
- Treat newer models as options, not automatic upgrades, if the current quality and cost target is already met.

In public terms, the pipeline uses OpenAI transcription followed by GPT-based cleanup. The detailed private prompts, exact deployment configuration, and operational secrets are not part of this public page.

## Windows Client

The Windows client is a packaged executable with a taskbar- and tray-friendly workflow. It supports global hotkeys, microphone selection, an input level meter, recording and processing timers, clipboard copy, and AppData-based persistence.

Default hotkeys:

- `Ctrl+F12`: show/hide
- `Ctrl+F11`: start recording
- `Ctrl+F10`: stop and send

Status: complete and usable.

## Android Client

The Android app is also named **Personal Voice Keyboard**.

Implementation notes:

- Package: `com.pvk.voicekeyboard`
- Minimum SDK: API 28
- Kotlin + Jetpack Compose
- Proxy configuration persistence via DataStore
- SharedPreferences migration
- Runtime microphone permission
- Foreground-only recording
- MediaRecorder-based audio capture
- Input level meter
- Recording and processing timers
- Adaptive timeout
- Retry/discard without losing recorded speech
- Pending recording preservation
- Quick Settings tile
- Compact translucent quick capture activity

The primary Android flow is tile-first: open the Quick Settings tile, launch the compact capture activity, auto-start recording when configuration and permission are available, stop and send, copy the result to the clipboard, and return to the previous task.

Status: Android v1 is stable enough for daily personal use.

## Security and Privacy

This is currently a personal-use tool, not a public service or open-source release.

Security and privacy boundaries:

- The OpenAI API key is stored only in Cloudflare Worker secrets.
- Windows and Android clients do not contain OpenAI API keys.
- Clients store only the proxy URL and proxy token.
- Audio is sent to the proxy for transcription and cleanup.
- Source code is currently private.
- Actual proxy tokens, OpenAI keys, full internal prompts, exact private deployment details, logs, and private repository paths are not published.

## Development Workflow

I treated AI-assisted development as a structured product loop rather than a one-shot code generation task. I set product direction and tested the tool in real use; ChatGPT helped with architecture and planning; Codex handled implementation; and daily usage determined the next patch.

The loop was effective because the roles were explicit:

- **User:** product direction, UX testing, and real-world judgment.
- **ChatGPT:** architecture, planning, prompt design, and debugging strategy.
- **Codex:** implementation and builds.
- **Real daily use:** validation of what mattered next.

## What I Learned

- The most important metric was not raw model latency, but total user time: waiting plus manual correction.
- A serverless proxy was the right architectural choice because it protected API keys and centralized model policy.
- The same proxy improved both Windows and Android clients without client rebuilds.
- Glossary-aware prompting solved practical terminology problems without enabling expensive search by default.
- Real daily use was a better guide than abstract feature planning.
- AI-assisted development works best when roles are explicit: human decides, ChatGPT plans, Codex implements, and real usage verifies.

## Current Status

Personal Voice Keyboard is complete and usable as a private personal workflow.

The initial CLI/reference project is frozen as a quality baseline. The serverless proxy is active as the shared transcription and cleanup layer. The Windows client is packaged and usable. The Android v1 app is stable enough for daily personal use.

## Future Work

Possible future directions include:

- Optional public release.
- Privacy policy and Play Store preparation.
- Better onboarding for non-technical users.
- Optional glossary editor.
- Optional search fallback for uncertain proper nouns.
- Realtime voice scratchpad exploration.
- More polished Android capture UI.
- Possible widget or IME exploration.

## Personal Note

I want to leave a small note to myself here: congratulations on finishing this one.

This project began with a very practical frustration. Even typing a message to an LLM often felt like friction, especially on a phone. I wanted to talk to LLMs more like I think: freely, at length, with corrections handled after the thought was spoken rather than before it was written.

The clipboard-first design became the key. The tool does not immediately send my words into one specific app. It turns speech into cleaned text, puts it on the clipboard, and lets me decide where it goes. That small detail changed the feeling of the whole workflow.

Ironically, this started because I was impressed by ChatGPT-style voice input. After building this, I often prefer my own tool: I can speak for a long time, preserve technical terms, review the cleaned result, edit if needed, and paste it anywhere. It feels less like “dictation” and more like giving my thoughts directly to the computer.
