---
name: second-pass
description: Pressure-test a finished written artifact (plan, spec, decisions) before relying on it — checking goal alignment, internal soundness, and (when a reference is named: guideline, spec, template, checklist) complete adherence to it. Proposes only surgical, evidence-backed changes for real gaps; proposing nothing is a valid outcome. Use when asked to second-pass, double-check, sanity-check, QA, or stress-test a plan, spec, or set of decisions. For written artifacts, not code.
---

# Second Pass

You are checking a finished artifact, not improving it. Hold it as sound until a specific, named defect proves otherwise. Finding nothing that warrants a change is a successful run.

## Phase 0 — Anchor

State the goal the artifact must serve, in one sentence. Take it from the session if the artifact was produced here.

**Gate:** if the goal is not clear, ask. Never infer a goal and proceed. **Exception:** if the request scopes the check to internal soundness only, skip the goal and the alignment axis, and say so in the report.

If the request names a reference (guideline, spec, template, checklist), load it. Every requirement in it is mandatory.

## Phase 1 — Map

List the assumptions, decisions, and conclusions the rest of the artifact rests on. Spend your scrutiny there. Note everything else as detail.

## Phase 2 — Detect

Try to break the artifact. Over-generate candidates. Defend nothing yet.

- **Alignment:** does it achieve the Phase 0 goal, or quietly solve an adjacent problem?
- **Soundness:** are the load-bearing assumptions valid? Does the reasoning support the conclusions? Missing cases, contradictions?
- **Conformance** (only with a reference): walk every requirement and flag each one not met. Each is a candidate regardless of the relevance floor.

**Relevance floor:** a candidate must bear on alignment, soundness, or correctness. Drop style, wording, and formatting silently.

**Gate:** finish the full candidate list before Phase 3.

## Phase 3 — Steelman

Try to kill each candidate. It dies only if you can:
- quote or cite **text in the artifact** that resolves it, or
- show it is **inert**: nothing downstream changes whether it is fixed or not.

"Probably fine" kills nothing. A conformance candidate can only die by citing where the requirement is met.

A candidate survives when it is unresolved and consequential.

## Phase 4 — Propose

For each survivor, write the smallest edit that closes the gap.

**Gate:** propose, do not apply. If closing a gap needs substantial rewriting, say so and describe it. Do not expand scope.

## Phase 5 — Report

Write for a reader outside the project. Plain words. For each finding: what is wrong, what breaks because of it, and the fix. No unexplained terms from the artifact.

1. **Goal.** The one line you checked against.
2. **Findings.** Each survivor: the gap, what breaks downstream, the proposed edit.
3. **Dismissals.** Every dropped candidate, load-bearing first, one line each: the candidate and why it died (cited text, or inert).
4. If nothing survived: say "Checked against the goal and for internal soundness; no load-bearing gaps found", list the dismissals, and stop.

One pass. Do not review your own output.
