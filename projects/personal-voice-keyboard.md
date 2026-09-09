---
layout: default
title: Personal Voice Keyboard
description: A private AI dictation system for Windows and Android.
permalink: /projects/personal-voice-keyboard/
---

# Personal Voice Keyboard

*A private AI dictation system for Windows and Android.*

**Personal Voice Keyboard** is a private AI dictation system I built and use daily on Windows and Android. It turns Korean-English mixed speech into cleaned, paste-ready text through a shared serverless proxy and copies the result to the clipboard.

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
Quick Settings tile -> Overlay capture -> Stop & Send -> Clipboard -> Paste
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

Model choices are informed by blind comparisons using my own speech samples, considering output quality, latency, and cost.

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

Daily use revealed that long recordings could produce incomplete transcripts even when requests completed successfully.

- Long recordings are transcribed in overlapping chunks and combined before a single cleanup pass.
- The latest source recording is retained locally, with retry and discard controls for recovery after processing failures.

Default hotkeys:

- `Ctrl+F12`: show/hide
- `Ctrl+F11`: start recording
- `Ctrl+F10`: stop and send

Status: In daily use; actively maintained.

## Android Client

The Android app is also named **Personal Voice Keyboard**.

Implementation notes:

- Package: `com.pvk.voicekeyboard`
- Minimum SDK: API 28
- Kotlin + Jetpack Compose
- Proxy configuration persistence via DataStore
- SharedPreferences migration
- Runtime microphone permission
- Foreground microphone service with a recording notification
- MediaRecorder-based audio capture
- Input level meter
- Recording and processing timers
- Adaptive timeout
- Retry/discard without losing recorded speech
- Pending recording preservation
- Quick Settings tile
- An overlay panel that lets me keep interacting with the underlying app while recording

The Quick Settings tile opens an overlay capture panel. Microphone and overlay permissions are explicit, and I can keep touching and scrolling the underlying app while recording.

Status: In daily use; actively maintained.

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

I use AI-assisted development as a structured product loop rather than a one-shot code generation task.

- **Me:** Product requirements, UX, final architecture and security decisions, model evaluation, and daily-use validation.
- **ChatGPT:** Design exploration, trade-off analysis, and review.
- **Codex:** Scoped implementation, testing, builds, and deployment.

Daily use determines the next patch.

## What I Learned

- The most important metric was not raw model latency, but total user time: waiting plus manual correction.
- A serverless proxy was the right architectural choice because it protected API keys and centralized model policy.
- The same proxy improved both Windows and Android clients without client rebuilds.
- Glossary-aware prompting solved practical terminology problems without enabling expensive search by default.
- Real daily use was a better guide than abstract feature planning.
- AI-assisted development works best when human decision-making, AI support, and real-use validation are explicit.

## Current Status

In daily use on Windows and Android. Actively maintained; source code is private.

The initial CLI/reference project is frozen as a quality baseline. The serverless proxy is active as the shared transcription and cleanup layer. The Windows client is packaged and usable. The Android app is in daily personal use.

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
