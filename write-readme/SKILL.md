---
name: write-readme
description: Write or update a public repo's README in plain language — what it is, what problem it solves, and how to use it, with every step verified against the repo's actual files. Use when the user wants a README created or refreshed, or says "write a readme", "update the readme", or "readme this repo".
---

# Write README

Reader: a stranger who found the repo and wants to know what it is and how to run it. They may be new to the tools involved.

## Language

- **Plain words.** If a word would not appear in a newspaper, replace it or explain it in the same sentence. No unexplained acronyms or tool names.
- **Short.** One idea per sentence. Under 20 words. Cut any sentence that does not help the reader understand or run the project.
- **Say what it does, not how impressive it is.** No adjectives the repo cannot prove. "Turns a CSV into a chart" beats "a powerful visualisation tool".
- **Steps are commands.** Each how-to step is one command in a code block, with one plain sentence on what it does and what the reader will see.

## Phase 1 — Inventory

Read, in order: manifests and lockfiles (`package.json`, `pyproject.toml`, `requirements.txt`, or equivalent); the entry points and scripts they reference; `.env.example` and config files, then grep the code for which variables it reads; the existing README; CLAUDE.md and project docs, for intent only.

**Gate — privacy:** CLAUDE.md, memories, and private notes inform intent only. Nothing from them goes into the README. No secrets or real key values. Placeholders only.

**Gate — grounding:** if what the repo is and does cannot be grounded in its code, docs, or the current session, ask the user. Never invent the purpose.

## Phase 2 — Verify

Every instruction must trace to something in the repo right now: a command to a script or binary, an env var to code that reads it, a version to a manifest pin, a path to a file in the tree.

Do not execute anything unless the user asks in this invocation.

**Gate:** an untraceable instruction stays out and goes in the report as unconfirmed.

## Phase 3 — Draft

Template, in order. Omit any section with nothing verified to say.

1. **Title and intro.** Two or three sentences: what it is, what problem it solves, who it is for.
2. **How to use.** Prerequisites with versions, install, run, expected result. Copy-pasteable.
3. **Configuration.** Only variables the code reads. Placeholder values.
4. **Status and license.**

If the repo is not a runnable program (skills, docs, config), "How to use" becomes how to install or use its contents. Same verification standard.

On an update: bring the existing README to this template. Carry over user-added images, badges, and links. Drop a link only when it is visibly stale, and record every drop for the report.

## Phase 4 — Check

- A reader with zero context reaches a working state using only this document.
- What it is and what it solves are clear before scrolling.
- No secrets, real keys, or private context.

Fix every failure before presenting.

## Phase 5 — Report

State what was verified and against which files, what was left out as unconfirmed, and on an update, what was carried over or dropped and why.
