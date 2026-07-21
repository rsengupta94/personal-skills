---
name: write-readme
description: Write or update a public repo's README — a concise what-it-is intro plus run instructions verified against the repo's actual files. Use when the user wants a README created or refreshed, or says "write a readme", "update the readme", or "readme this repo".
---

# Write README

Two readers: someone evaluating the author's work (primary), and a stranger trying to run the repo. Brevity serves both — every sentence must earn its place for one of them.

Run the phases in order. Honor every gate.

## Phase 1 — Inventory

Read, in this order:
- Manifests and lockfiles (`package.json`, `pyproject.toml`, `requirements.txt`, or equivalent): name, scripts, dependencies, version pins
- Entry points and scripts the manifests reference
- `.env.example` and config files, then grep the code for which variables it actually reads
- The existing README, if one exists
- CLAUDE.md and project docs — for intent only

**Gate — privacy:** CLAUDE.md, memories, and private notes inform intent only; no content from them goes into the README. The README is public; they are not. Never include secrets or real key values — placeholders only.

**Gate — grounding:** if what the repo is and does cannot be grounded in its code, docs, or the current session, ask the user for it. Never invent the purpose.

## Phase 2 — Verify statically

Every instruction that will appear in the README must trace to a repo artifact that exists right now:
- A command → a script or binary defined in the repo (`npm run dev` requires a `dev` script in `package.json`)
- An env var → a place in the code that reads it
- A version requirement → a manifest pin, not a guess
- A referenced file or path → present in the tree

Do not execute anything — no installs, no runs — unless the user explicitly instructs it in this invocation.

**Gate:** an instruction that cannot be traced does not go in. If a step seems necessary but is unverifiable, leave it out and list it in the Phase 5 report as unconfirmed.

## Phase 3 — Draft

If a README exists, bring it fully up to this template and style contract — the same standard as a fresh write. Carry over user-added assets (images, badges, external links); record each drop for the report. An external URL cannot be traced statically: drop it only when it is visibly stale (points to a renamed file, old repo name, or removed feature); otherwise carry it over and list it as unconfirmed in the Phase 5 report.

Template, in order — omit any section with nothing verified to say. Section names describe content, not literal headings:

1. **Title + one line** — what it is. No adjectives. No dedicated problem statement anywhere — if purpose needs context, a single sentence here carries it; specificity persuades, not framing.
2. **What it does** — concrete capabilities, one usage example.
3. **Quickstart** — prerequisites with versions, install, run, expected result. Copy-pasteable.
4. **Configuration** — only variables the code reads. Placeholder values.
5. **How it works** — one paragraph, only when the design is non-obvious. This section serves the evaluating reader: decisions and why, not narration.
6. **Status / license.**

If the repo is not a runnable program (a skills collection, docs, config), Quickstart becomes how to install or use its contents — same verification standard.

## Phase 4 — Self-check

- **Fresh-clone test:** a reader with zero context reaches a working state using only this document.
- **First-screen test:** what it is, what it does, and who it's for are clear before scrolling.
- **Fluff scan:** delete every banned word — powerful, seamless, robust, leverage, cutting-edge, blazing(ly), effortless(ly), revolutionize, supercharge — and any adjective the repo can't prove. Delete any sentence that doesn't help the reader decide to read on, install, or leave.
- **Plain-language scan:** short sentences, common words. Technical terms stay when they are the accurate name for the thing; drop jargon a plainer word can fully replace.
- **Leak scan:** no secrets, no real key values, no private context.

Fix every failure and re-run the failed check before presenting.

## Phase 5 — Report

Alongside the README, state:
1. What was verified, and against which files.
2. What was left out as unconfirmed, so the user can confirm and add it.
3. On an update: what was carried over, what was dropped and why.
