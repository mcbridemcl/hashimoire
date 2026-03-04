# hashimoire

A practical, field-tested reference for DFIR and defensive security work: tool install notes, repeatable workflows, artifact paths, and the commands I actually use (not a copy of `--help` output).

## What this is

This repo is my living field tome/grimoire for:
- DFIR triage and evidence handling habits
- Tool installation and usage notes
- Common command patterns (Nmap, awk, PowerShell, hashing, etc.)
- Detection and hunting queries (SIEM-focused)
- Defensive OSINT and exposure checking
- Templates and checklists that keep work consistent

## What this is not

- Not a hacking tutorial.
- Not exploit development.
- Not stealth, evasion, persistence, credential theft, or “how to break in” guidance.
- Not case-specific content. No sensitive details, no client data, no internal systems.

If something feels like it could be used primarily to harm people, it does not belong here.

## How to use this repo

- Start with **Snippets** for quick “I forgot the flags” refreshers.
- Use **Playbooks** when you need repeatable workflows under time pressure.
- Use **Docs** for deeper notes, installs, gotchas, and artifact references.
- Use **Detections** for SIEM queries and tuning notes.

### Tagging conventions (used in pages)

Most pages include quick tags near the top:

- **Use case:** triage | hunting | validation | response
- **Environment:** windows | linux | macos | cloud
- **Risk:** safe | caution

“Caution” means: double-check scope, permissions, and impact before running.

## Contents

- [Repo structure](#repo-structure)
- [Quick start](#quick-start)
- [Quality bar](#quality-bar)
- [Contributing](#contributing)
- [License](#license)
- [Disclaimer](#disclaimer)

## Repo structure
```text
/
├─ docs/
│  ├─ tools/
│  │  ├─ volatility/
│  │  ├─ ftk-imager/
│  │  └─ ...
│  ├─ windows/
│  ├─ linux/
│  └─ ...
├─ playbooks/
│  ├─ triage/
│  ├─ collection/
│  └─ ...
├─ snippets/
│  ├─ nmap.md
│  ├─ awk.md
│  ├─ powershell.md
│  ├─ hashing.md
│  └─ ...
├─ detections/
│  ├─ splunk/
│  ├─ sentinel/
│  ├─ elastic/
│  └─ ...
├─ osint/
│  ├─ exposure-checks.md
│  └─ ...
├─ templates/
│  ├─ case-notes-template.md
│  ├─ chain-of-custody-template.md
│  └─ ...
└─ scripts/
   ├─ windows/
   └─ linux/

```
## Disclaimer

This content is provided for authorized, legal, and ethical defensive use only. You are responsible for complying with your organization’s policies and all applicable laws. Always verify scope and permissions before collecting data or running commands.
