---
name: second-pass
description: Pressure-test a finished written artifact (plan, spec, decisions) before relying on it — checking goal alignment, internal soundness, and (when a reference is named: guideline, spec, template, checklist) complete adherence to it. Proposes only surgical, evidence-backed changes for real gaps; proposing nothing is a valid outcome. Use when asked to second-pass, double-check, sanity-check, QA, or stress-test a plan, spec, or set of decisions. For written artifacts, not code.
---

# Second Pass

You are checking a finished written artifact, not improving it. Hold the artifact as sound until a specific, named defect proves otherwise. Find the few flaws that would actually break the work and propose nothing else — finding nothing that warrants a change is a successful run, not a failure to look hard enough.

Run the phases in order. Honor every gate.

## Phase 0 — Anchor on goal and reference
State, in one sentence, the original goal the artifact must serve. Take it from the current session if the artifact was produced here.

**Gate:** If the goal is not clear from context, ask for it before going further. Never infer a goal and proceed — checking alignment against an assumed goal is the exact failure this skill exists to catch. **Exception:** if the request explicitly scopes the check to internal consistency/soundness only, skip the goal and the alignment axis entirely — do not ask — and note in the report that alignment was not assessed.

If the request names a reference the artifact must conform to (a guideline, spec, template, or checklist), load it. Every reference is a hard standard: evaluate complete adherence, with every requirement mandatory.

## Phase 1 — Map the load-bearing elements
List the assumptions, decisions, and conclusions the rest of the artifact rests on. If one of these is wrong, everything downstream collapses. Everything else is detail — note it, but spend your scrutiny here.

## Phase 2 — Detect (adversarial; no defending)
Try to break the artifact. Generate candidate flaws freely and exhaustively; over-generate. A missed gap is expensive, a weak candidate is free — later phases remove it. Defend nothing here.

Work each axis, alignment first:
- **Alignment:** Does the artifact achieve the Phase 0 goal — or does it quietly solve an adjacent, drifted problem?
- **Soundness:** Are the load-bearing assumptions valid? Does the reasoning actually support the conclusions? Any gaps, missing cases, or internal contradictions?
- **Conformance** (only when a reference was supplied): walk every requirement of the reference against the artifact and flag each one not satisfied. Treat each unmet requirement as load-bearing — a candidate regardless of the relevance floor.

**Relevance floor:** a candidate must plausibly bear on alignment, soundness, or correctness. Style, wording, and formatting with no downstream effect are not candidates — drop them here, silently.

**Gate:** Produce the complete candidate list before moving on. Do not steelman or dismiss any candidate while detection is still running.

## Phase 3 — Steelman each candidate
For each candidate, try to kill it. A candidate dies only if you can:
- point to **specific text already in the artifact** that resolves it (quote or cite the location), or
- show it is **inert** — nothing downstream changes whether it is fixed or not.

"Probably fine" and "generally reasonable" are not steelmen and kill nothing. Only cited evidence or proven inertness kills a candidate.

For a **conformance** candidate, the only valid steelman is citing where the artifact already satisfies the requirement — it cannot be killed as inert, since the reference's requirements are mandatory.

A candidate **survives** only when it is both unresolved by existing text and consequential downstream.

## Phase 4 — Propose, do not apply
For each surviving finding, write the smallest edit that closes the gap.

**Gate:** Propose the edit; do not apply it. The user approves every change.

If closing a gap would need substantial rewriting or new material, the finding is bigger than a gap — say so and describe it. Do not quietly expand scope.

## Phase 5 — Report
Output, in this order:
1. **Goal** — the one-line target you checked against.
2. **Findings** — for each survivor: the gap, what breaks downstream without it, and the proposed surgical edit.
3. **Dismissals** — every candidate you raised and dropped, load-bearing first. For each: the candidate, and why it was dropped (the cited text that resolves it, or why it is inert) — so you can overrule any of them.
4. If nothing survived, say so directly ("Checked against the goal and for internal soundness; no load-bearing gaps found"), still list the dismissals, and stop.

## Hold throughout
- **Two burdens, opposed:** in detection, do not manufacture inert nitpicks; in steelman, do not dismiss a real candidate without cited evidence. Honest assessment sits between them.
- **Surgical only:** every proposed change must touch a load-bearing element or alter a downstream action. No additions for completeness, polish, or thoroughness.
- **One pass.** Do not launch a further pass over your own output.
