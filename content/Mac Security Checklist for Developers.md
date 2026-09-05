---
title: "Mac Security Checklist for Developers"
created: 2026-09-05
tags:
  - macos
  - security
  - checklist
---

> *A five-minute, read-only checklist to confirm macOS's built-in protections are actually switched on, plus a scan for the persistence tricks malware commonly relies on.*

Most Macs already ship with strong protections — System Integrity Protection, Gatekeeper, XProtect, FileVault, a firewall. The problem is rarely "my Mac lacks security tools," it's that one of these got switched off at some point (often by an installer, or a "just this once" troubleshooting step) and never got switched back on.

This is a one-time (then periodic) check, not something you install and forget. Nothing here requires third-party software.

## Run the checklist

Paste this into Terminal. It's entirely read-only — it reports status, it doesn't change anything on your machine.

```bash
echo "=== SIP status ==="
csrutil status

echo
echo "=== FileVault status ==="
fdesetup status

echo
echo "=== Firewall status ==="
/usr/libexec/ApplicationFirewall/socketfilterfw --getglobalstate

echo
echo "=== Gatekeeper status ==="
spctl --status

echo
echo "=== User LaunchAgents (~/Library/LaunchAgents) ==="
ls -la ~/Library/LaunchAgents 2>/dev/null

echo
echo "=== System LaunchAgents (/Library/LaunchAgents) ==="
ls -la /Library/LaunchAgents 2>/dev/null

echo
echo "=== System LaunchDaemons (/Library/LaunchDaemons) ==="
ls -la /Library/LaunchDaemons 2>/dev/null

echo
echo "=== Login items ==="
osascript -e 'tell application "System Events" to get the name of every login item'
```

## What you're looking for

| Check | Good result | If it's not |
|---|---|---|
| SIP | `System Integrity Protection status: enabled.` | Re-enable via Recovery Mode: `csrutil enable`. Something disabled it deliberately — figure out why before re-enabling if you don't recognize the reason. |
| FileVault | `FileVault is On.` | System Settings → Privacy & Security → FileVault → Turn On. Protects your data if the machine is lost or stolen. |
| Firewall | `Firewall is enabled. (State = 1)` | `sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate on`, or System Settings → Network → Firewall. Blocks unsolicited inbound connections; doesn't affect normal browsing. |
| Gatekeeper | `assessments enabled` | System Settings → Privacy & Security → Security → set "Allow applications from" appropriately. Blocks unsigned/unnotarized apps from running by default. |
| LaunchAgents / LaunchDaemons | Only entries you recognize (Chrome/Google updaters, Dropbox, your VPN client, etc.) | Anything unfamiliar is worth investigating before assuming it's fine — search the label name, check what binary it launches (`plutil -extract Program raw -o - <path>`), and whether that binary is code-signed (`codesign -dv <path>`). |
| Login items | Only apps you intentionally added | Remove anything you don't recognize via System Settings → General → Login Items & Extensions. |

## Everyday hygiene that matters more than any tool

- Avoid `curl | bash` installs and unsigned `.pkg`/`.dmg` downloads from random sites — prefer Homebrew or the App Store.
- Don't routinely strip the quarantine flag (`xattr -d com.apple.quarantine`) from downloaded files just to get past a Gatekeeper prompt — that prompt exists for a reason.
- As a developer specifically: be wary of malicious npm/pip packages, and glance at `pre`/`postinstall` scripts before running `npm install` on an unfamiliar repo.
- Re-run this checklist after any major troubleshooting session where you disabled something "temporarily" — that's the most common way these protections end up off for months.

## Optional: deeper scan for developers

The checklist above covers OS-level settings. A more thorough scan would also check for things like VS Code auto-run task exploits, files disguised as fonts/images, and npm/pip install scripts that shell out to `curl`/`eval`/`base64` — that's a separate, more involved script worth building if this checklist turns up something, or if you regularly clone unfamiliar repos.
