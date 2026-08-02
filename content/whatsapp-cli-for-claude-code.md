---
title: "Give Claude Code a WhatsApp Skill"
created: 2026-08-02
tags:
  - claude-code
  - whatsapp
  - cli
  - ai-workflows
---

> *A free, open-source CLI plus one skill file turns Claude Code into something that can read, search, and send your WhatsApp messages, no bot number, no API key, no cloud middleman.*

I just wired this up and it's working superbly well. If you live half your working day in Claude Code and the other half fielding WhatsApp messages, this closes the gap.

## The tool: whatsapp-cli

[eddmann/whatsapp-cli](https://github.com/eddmann/whatsapp-cli) is a standalone Go binary that speaks the WhatsApp Web multi-device protocol directly, no bot account, no Twilio, no paid API. It links to your existing WhatsApp account the same way WhatsApp Web or Desktop does, then mirrors your chats into a local SQLite database.

```bash
brew install eddmann/tap/whatsapp-cli
whatsapp auth login    # scan the QR code once, session persists ~20 days
whatsapp sync           # pull message history into the local database
```

Every command returns structured JSON, which is exactly what makes it a good fit for an LLM to drive: no scraping, no screenshotting a phone.

## The skill: pointing Claude Code at it

The CLI alone doesn't help Claude Code, it needs to know the tool exists and how to use it. That's what a Claude Code **skill** is for: a markdown file describing when to reach for a tool and what the command surface looks like.

Drop a `SKILL.md` in `~/.claude/skills/whatsapp/` with the command reference (`chats`, `messages`, `search`, `send`, `forward`, `react`, `groups`, `contacts`), and Claude Code picks it up automatically whenever a prompt looks WhatsApp-shaped, "did John reply about the invoice?", "send the team the deploy is done", "search my chats for that tracking number."

```bash
whatsapp context                 # connection status + recent chats, one call
whatsapp search "invoice" --timeframe this_week
whatsapp send <JID> "Deploy is done" --reply-to <MSG_ID>
```

## Why it's worth setting up

- **Local-first.** Messages live in a SQLite database on your machine, not a third-party server.
- **No bot identity.** It links as a device on your real account, so messages Claude sends look like they came from you, because they did.
- **Zero ongoing cost.** No per-message API fees, no subscription, MIT-licensed.
- **JSON everywhere.** Structured output means Claude doesn't have to guess-parse chat text, JIDs, timestamps, and message types are all typed fields.

## The catch

- Auth is a **linked device**, not a bot, so it rides on your personal WhatsApp session and needs re-linking roughly every 20 days.
- It's read/write to your *real* chats. Test `send` on a chat with yourself before pointing Claude at a group.
- There's a separate, unrelated project (`whatsapp-claude-plugin`, an MCP server that lets you message *into* Claude Code from your phone) that solves a different problem, don't confuse the two if you go looking.

## The takeaway

Most "connect an LLM to WhatsApp" setups mean standing up a bot number and a webhook. This is the opposite: a local binary, one skill file, and Claude Code already knows how to read and act on your actual chats.

*Source: [eddmann/whatsapp-cli on GitHub](https://github.com/eddmann/whatsapp-cli).*
