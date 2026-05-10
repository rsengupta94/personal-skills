---
name: explain-tfd
description: Translate a TFD (Technical Feasibility Document) for a Product Manager — a plain-language walkthrough of decisions plus a concise stakeholder-conversation kit. Use when the user shares a TFD or says "explain the TFD", "understand this TFD", or "brief me on the TFD".
---

# Explain TFD

Do not critique the TFD. Do not flag gaps, suggest improvements, or predict risks the doc did not raise.

## Step 1 — Locate the TFD

The PM has either shared a file or pasted TFD content into the chat.

To find a file: scan the working directory (case-insensitively) for any filename containing `TFD` or a variant of `Technical Feasibility Document` — hyphenated, underscored, camel-cased, spaced, or with prefixes/suffixes (e.g. `feature-x-tfd.pdf`, `Technical_Feasibility_Document_v2.docx`, `TechnicalFeasibilityDocument.md`). Read the full content.

If multiple files match, ask the PM which one. If nothing matches and nothing was pasted, ask the PM for the filename or to paste the content. Do not proceed until you have the content.

## Step 2 — Identify key decisions

A "key decision" is a choice that affects timeline, scope, cost, vendor relationships, or that an internal business stakeholder (exec to mid-level leader) might ask about. Examples: build vs buy, vendor selection, tech stack picks with business consequence, scaling architecture, phasing, third-party dependencies.

Skip pure implementation detail: linting rules, file structure, naming conventions, internal libraries, code organization, language-specific patterns.

Cap at 7. If fewer than 5 stakeholder-relevant decisions exist, list what is there; do not pad to hit a number.

## Step 3 — Resolve the rationale for each decision

- If the TFD states the rationale, use it.
- If the TFD does NOT state it, use industry knowledge to explain why teams typically make this choice. Mark this entry inline as inferred and tell the PM to verify with the engineer.

Assume the PM knows only surface-level technical terms (API, database, server, cache). Define anything more specific in the same sentence.

## Step 4 — Produce two artifacts, in this order

### Walkthrough (≤600 words, bullet-heavy)

    ## What's being built
    [One short paragraph in plain language. Translate the technical scope for a PM.]

    ## Key decisions
    [Up to 7. One list, ordered by stakeholder importance. Each entry uses one of these two formats based on whether the rationale was stated:]

    - **[Decision in plain language]**
      - Why: [Rationale from the TFD]

    - **[Decision in plain language]**
      - Why: [Inferred rationale] — *not stated in the TFD; verify with the engineer.*

### Briefing

    ## 30-second pitch
    [~75 words. What's being built and the headline approach. Plain language, narratable verbatim.]

    ## Likely stakeholder questions
    [3–4 questions a non-technical business stakeholder is most likely to ask. For each:]
    - **Q: [Question]**
      - A: [40–60 words. Explain what was decided and why — never how to push back on it.]

## Failure modes

- **TFD not found and nothing pasted**: Ask for the filename or content. Do not invent.
- **TFD has no stakeholder-relevant decisions, only implementation walkthrough**: Tell the PM plainly. Do not pad to fill the template.
- **TFD is sparse**: Surface what is there. Do not invent decisions.
