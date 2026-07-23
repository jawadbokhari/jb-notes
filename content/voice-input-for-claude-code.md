---
title: "A Better Way to Talk to Claude Code (Mac Only)"
created: 2026-07-23
tags:
  - claude-code
  - voice-input
  - macos
  - ai-workflows
---

> *Claude Code's built-in voice input mangles long sentences. A free, local, open-source dictation app fixes it — if you're on a Mac.*

Claude Code has a voice input command. It also, frequently, doesn't understand what you actually said.

Short commands are fine. But the moment you try to think out loud — describe a bug across three sentences, or explain the shape of a refactor — it starts dropping clauses, mangling technical terms, and returning something that needs as much editing as if you'd just typed it yourself. For a tool meant to remove friction, it adds it right back.

The fix isn't a better prompt. It's a better microphone-to-text pipeline in front of Claude Code entirely.

## The tool: OpenSuperWhisper

[OpenSuperWhisper](https://github.com/starmel/OpenSuperWhisper) is a free, open-source dictation app for Mac. It runs OpenAI's Whisper speech-to-text model **entirely locally** — no account, no API key, no per-minute cost, no audio ever leaving your machine. Hold a hotkey, talk, release, and the transcribed text gets typed wherever your cursor is — including straight into a Claude Code prompt.

Because it's a general system dictation tool rather than something built into Claude Code's own voice command, it isn't limited by whatever narrower speech model Anthropic ships. It also just performs better in practice, particularly on longer, more complex sentences.

**Why it's worth trying**

- **Genuinely free.** MIT-licensed, runs whisper.cpp under the hood, no subscription or usage fees.
- **Fully local.** Nothing is sent to a cloud API — relevant if you're dictating anything sensitive.
- **Model choice.** You pick the Whisper model size — trading accuracy for speed/memory footprint.

## The catch: it's Mac-only

This is the one thing to flag before anyone gets excited: **OpenSuperWhisper only runs on Apple Silicon Macs (M1 and later), on macOS 14+.** Intel Macs aren't supported, and there's no Windows or Linux build — Intel/cross-platform support is listed as an open contribution goal, not a shipped feature.

If you're on Windows, this isn't the tip for you — and honestly, you may not need it. Windows' built-in voice input (Voice Access / Windows Speech Recognition) is noticeably more reliable at parsing full sentences than Claude Code's own voice command, so the gap this tool closes on Mac may already be closed for you natively.

## System requirements (medium model)

OpenSuperWhisper lets you choose which Whisper model size to run locally. The **medium** model is the sweet spot for most people — meaningfully more accurate than "small," without the size and latency cost of "large":

| | Medium model |
|---|---|
| Disk space | ~1.5 GB download |
| RAM during use | ~2.1 GB |
| Hardware | Any Apple Silicon Mac (M1/M2/M3/M4) |
| Acceleration | Runs on the Apple Neural Engine via Core ML — 3x+ faster than CPU-only |

There's no discrete GPU or VRAM requirement here — this isn't the CUDA/PyTorch version of Whisper people usually quote specs for. Any Apple Silicon Mac handles the medium model comfortably, Neural Engine included.

## The takeaway

- **If you're on an Apple Silicon Mac** and find Claude Code's voice command butchering your sentences, install OpenSuperWhisper, set it to the medium model, and dictate into Claude Code through it instead of through Claude's native voice command.
- **If you're on Windows,** stick with the OS-level dictation you already have — it's doing the job OpenSuperWhisper does for Mac users, natively.

Sometimes the fix for a bad feature isn't a better version of that feature — it's routing around it with a tool that was never trying to be an AI product in the first place.

*Sources: [Starmel/OpenSuperWhisper on GitHub](https://github.com/starmel/OpenSuperWhisper), [whisper.cpp model reference](https://github.com/ggml-org/whisper.cpp).*
