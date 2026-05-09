# Learning: Claude Code Skills

A personal one-stop reference. Updated only on explicit command. Kept lean.

## Goal
Understand skills well enough to (1) use custom skills confidently and (2) build my own when needed.

## Core concepts

### Mental model
Claude has a **menu of named behaviors**. Each entry = `name` + `description`. The full recipe (the SKILL.md body) loads only when the moment calls for it — either via `/<name>` or because user intent matches the description.

A skill is **a markdown file of instructions Claude reads on demand**. Not code, not a runtime mode — just a behavior recipe Claude follows. Skill ≠ tool ≠ subagent ≠ slash command ≠ hook.

| Primitive | What it does |
|---|---|
| **Skill** | Instructions Claude reads & follows |
| **Tool** | Code the harness executes (Read, Bash, MCP) |
| **Subagent** | Separate Claude instance with own context |
| **Slash command** | Canned prompt expansion |
| **Hook** | Shell command triggered on events |

### Two superpowers
- **Lazy loading** — only `name` + `description` are visible at session start; the body loads only when invoked. Lets you install many skills without bloating context.
- **Description-based matching** — the `description` field is the entire matching surface. Vague description → skill never auto-activates. Precise description with trigger phrases (e.g. *"Use when user says 'review my plan'"*) → fires exactly when intended.

### Why skills exist (vs alternatives)
- Re-explaining each session → wastes time/tokens, drifts.
- Stuffing into `CLAUDE.md` → loaded always, doesn't scale.
- Building a custom tool/agent → heavyweight, needs code.
- Skill = packaged, reusable, only-when-relevant instructions.

### How the instructions actually behave
- Once loaded, the skill body is just text in conversation history.
- Claude is **strongly biased** by it, not deterministic — newer instructions can override; vague instructions drift.
- Multiple skills loaded in a session coexist (no "active skill"). Conflicting skills create ambiguity.

### Lifecycle — there is no "unload"
The skill body sits in context until `/clear`, `/compact`, or context eviction. Practical levers, in order of frequency:
1. **Let it sit** — most skill bodies are tiny (tens to low-thousands of tokens); cost is negligible vs the 1M window.
2. **Tell Claude to move on** — newer instructions take precedence over older context.
3. **`/clear`** — wipes everything. Heavy hammer; use when starting a new task.
4. **New session** — same effect, preserves terminal scrollback.

Worth worrying when: skills that pull in large bundled files, strongly opinionated behavioral skills (e.g. one that forces ultra-terse output), or two skills with contradictory instructions loaded together.

### What skills can do (the shape of the work)
Upper bound = anything Claude can already do in a conversation. The taxonomy is about *shape*, not capability:

- **Behavior / mode shifts** — change how Claude operates. E.g. force ultra-terse output, always reply formally, always be skeptical of premises. Reshape, don't task.
- **Procedural workflows** — multi-step recipes. E.g. test-driven dev loop (red→green→refactor), structured bug-diagnosis recipe, interview-the-user pattern. The bulk of useful skills.
- **Transformations / artifact production** — produce or modify a concrete thing. E.g. turn current conversation into a PRD, scaffold pre-commit hooks, migrate code from one library/idiom to another.

Real skills often blend families (e.g. an interview that also updates a domain-glossary doc as it goes = workflow + artifact).

### Beyond pure prompts
- **Bundled files** — a skill folder can ship scripts, templates, reference docs. SKILL.md instructs Claude to load/run them. Turns a skill into a prompt + toolkit.
- **Composability** — skills can chain or build on each other (e.g. write a PRD → break it into tickets → implement each with TDD → diagnose failures).

### When a skill is *not* the right tool
- **One-off task** → just prompt directly.
- **Universal always-on rule** → put it in `CLAUDE.md`.
- **Needs new code execution Claude can't already do** → build a tool / MCP server first.
- **Trivially-stated behavior** ("be concise") → not worth the packaging overhead.

### Mental shortcut: should this be a skill?
Three questions. Three yeses → skill. Any no → use something else.
1. **Repeatable** — will I want this same behavior again?
2. **Non-trivial** — multi-step, opinionated, or easy to misremember?
3. **Bounded** — clearly applicable only sometimes (not always-on)?

## This repo's catalog
_(empty — will fill as we discuss)_

## How to build a skill

### The two fields that matter
- **`name`** — kebab-case, becomes `/<name>`. Short, action-oriented.
- **`description`** — the highest-leverage line in the entire skill. The whole matching surface for auto-invocation. Wrong here → the skill goes dormant.

### Writing a strong description

**Formula:** `[What it does, verb-led]. Use when [intent signals + literal phrases].`

**Best practices:**
- **Answer two questions:** WHAT it does + WHEN to reach for it.
- **Include both trigger types:**
  - *Intent-based* — "Use when user wants to ..." catches paraphrased prompts.
  - *Phrase-based* — "...or mentions 'X'" catches literal keywords.
- **Lead with a concrete action verb** ("Interview", "Generate", "Refactor") — not abstractions ("Helps with...").
- **State the stop condition** if non-obvious ("until shared understanding is reached").
- **Keep tight** — one or two sentences max. Past ~500 chars, visibility degrades.
- **No marketing fluff** ("powerful, intuitive..."). Zero filler.
- **Describe what triggers, not what doesn't** — negatives still read as triggers.

**Smell test:** Read it as if scanning a menu of 50 skills. Would it stand out for the right prompts? Not for the wrong ones?

### Why a strong description matters even if you only use `/<name>`
Mechanically, explicit invocation bypasses matching. But skipping a good description costs you:
- **Auto-activation when you forget the exact name** (biggest one).
- **Autocomplete clarity** in the `/` menu.
- **Self-documentation** when listing or sharing skills.

Explicit-only is the brittle path; good descriptions unlock fluid use.

### Optional frontmatter fields exist
`allowed-tools`, `argument-hint`, `model` — escape hatches, rarely needed. Defaults are fine.

### Writing the body — the actual instructions

**Mindset shift:** the body is a prompt addressed to Claude, not documentation for a human reader. No preamble, no purpose statements (that's the description's job), no theoretical writing — just instructions Claude will act on.

### Voice
- **Imperative throughout.** "Interview the user", "Walk down each branch", "Run the loop." Not "consider", "be mindful of", "think about".
- **Address Claude directly.** Skip "this skill helps...". Drop straight into commands.
- **Format serves action.** Headers/bullets are for unambiguous next steps, not aesthetics.

### Structure follows the shape of the work
Three families, three natural body shapes:
- **Behavior / mode shifts** → a few rules + constraints. Often <30 lines. Pattern: *"Do X. Don't do Y. Prefer this form when Z."*
- **Procedural workflows** → numbered phases with **explicit gates** between them ("Do not proceed until X"). The gate is what keeps Claude from racing through.
- **Transformations / artifacts** → procedure + clear format spec for the output. Often references a bundled template.

### Properties of strong bodies
1. **Imperative voice** throughout. Concrete verbs only.
2. **Concrete over abstract.** "Generate 3–5 ranked hypotheses" beats "think carefully about causes."
3. **Explicit stop conditions / gates** between phases. Without these, Claude rushes.
4. **Escape hatches** — what *overrides* the default path ("If the codebase has the answer, explore it instead of asking").
5. **Failure modes named.** "If you cannot do X, stop and say so. List what you tried." Pre-handles the failure case so Claude doesn't fake confidence.
6. **Examples for non-obvious patterns.** Show the format, don't describe it.
7. **Tagged conventions** for things to clean up later (e.g. unique prefix on debug logs → greppable removal).

### Smells that kill bodies
- **Documentation prose** — "This skill is designed to..." Wastes tokens, gives no instruction.
- **Vague verbs** — "consider", "think about", "be mindful of". Claude can't act on these reliably.
- **Restating the description** — already in context; don't repeat.
- **Universal knowledge** — "write good tests with clear assertions". Claude already knows. State only what's *specific to this skill*.
- **Edge-case sprawl** — handling every "but if X then Y then Z". Often the skill is doing too much; split it.
- **No gates** — bodies that list steps without stop conditions.
- **Decorative headers** — `## Overview` with nothing actionable underneath.

### Least instruction principle (and length norms)
Claude is competent. State only what *changes* its behavior — the non-default things, in the order you want, with the constraints you want.

- **Tight** (10–40 lines): behavior shifts, simple workflows.
- **Structured** (50–150 lines): full procedural workflows with multiple phases.
- **>200 lines is a smell** — either the skill is doing too much (split it), or it's micromanaging Claude on things it already does well (cut those parts). Push detail into bundled files instead.

### Authoring loop (bodies are tuned, not authored once)
1. Draft as you'd dictate to a competent junior — imperative, ordered, only the constraints you care about.
2. Read it back asking *"where will Claude get this wrong?"* — add a guardrail for each.
3. Strip everything Claude already knows.
4. Add gates between multi-step phases.
5. **Invoke the skill and watch what Claude does.** Where it deviates → sharpen the body. Skill bodies are prompts; prompts are tuned, not authored.

### Bundled files & progressive disclosure within a skill

A skill is **a folder, not a file**. Beyond SKILL.md, the folder can ship templates, reference docs, checklists, examples, and scripts. When the skill is invoked, only `SKILL.md` loads automatically — bundled files load on demand, when SKILL.md instructs Claude to read them.

#### Why bundle?
SKILL.md should stay tight. When the skill genuinely needs long templates, reference principles, executable checks, or example outputs, bundling lets you split them out and load each only when relevant.

#### The critical loading mechanic
- Bundled files are **not auto-loaded** when the skill activates.
- Bundled files are **not magically known** to Claude.
- They load only when SKILL.md tells Claude to read them — Claude issues a `Read` tool call at runtime.

A reference is really a runtime instruction. Vague references get skipped; strong, conditional references get followed reliably.

#### Split principle — what goes where
| Goes in SKILL.md | Goes in a bundled file |
|---|---|
| Always-relevant on invocation | Only sometimes relevant |
| Decision logic, gates, structure | Reference / template / lookup material |
| Short imperative instructions | Long, detail-heavy content |
| The "what to do" and "in what order" | The "what does the output look like" / "how do I check X" |

Think of SKILL.md as the table of contents + procedure; bundled files are the chapters Claude reads on demand.

#### Common patterns
A bundled file can be **anything Claude can read or run** from inside the skill folder — JSON configs, CSV lookups, Python scripts, schemas, fixtures, images, subfolders, whatever fits the need. The list below is descriptive (shapes that recur), not prescriptive (allowed types). Invent your own filenames when the need is novel.

- **Format / template files** (`TEMPLATE.md`, `<thing>-FORMAT.md`) — define exact output shape. Referenced at artifact-creation time.
- **Reference / principle files** (`refactoring.md`, `interface-design.md`) — long lists of design rules or domain knowledge consulted situationally.
- **Checklist files** (`CHECKLIST.md`) — end-of-task verification too long to inline.
- **Example files** (`EXAMPLES.md`) — show-don't-tell for tricky patterns.
- **Scripts** (`scripts/<name>.sh`) — deterministic checks or transformations Claude runs via Bash. How skills become more powerful than pure prompts.
- **Sub-skill briefs** (`AGENT-BRIEF.md`) — instructions for a sub-agent the skill dispatches.

#### Writing strong references in SKILL.md
| Weak (often skipped) | Strong (reliably followed) |
|---|---|
| "There's a TEMPLATE.md if you need it." | "Read TEMPLATE.md and follow the exact format." |
| "See REFERENCE.md for more info." | "Before answering, read REFERENCE.md sections relevant to the question." |
| "Examples are in EXAMPLES.md." | "If the input is ambiguous, read EXAMPLES.md and pick the closest match." |

Make references **imperative**, **conditional on a clear trigger**, and **specific about what to do with the file's contents**.

#### Structural idiom: `<what-to-do>` vs `<supporting-info>`
A clean way to make the split visible: wrap the imperative core in a `<what-to-do>` block and the reference material in a `<supporting-info>` block. Signals to Claude that the second block is "background to consult, not orders to execute." Not required, but tidy.

#### The fractal pattern (the deep idea)
Progressive disclosure recurs at two scales — same lazy-load principle, applied at two levels:

| Always loaded | Loaded on demand |
|---|---|
| Top level: skill *descriptions* | SKILL.md bodies |
| Within skill: SKILL.md | Bundled files |

This is what lets the system scale — hundreds of skills, dozens of reference files each, only the relevant slice ever in context.

#### When NOT to bundle
- SKILL.md fits comfortably under ~100 lines.
- "Reference" content is short enough to inline.
- Content is always needed (no real "sometimes" conditionality).

A 50-line skill with 4 bundled files is usually worse than the same content in one file. Bundling earns its keep when the body would otherwise exceed ~150–200 lines, or when scripts/templates need to be executable artifacts.

#### Trade-offs
- **Pro:** keeps SKILL.md focused; scales to complex skills; bundled scripts give deterministic capabilities prompts lack.
- **Pro:** loading is genuinely lazy — no token cost for unread files.
- **Con:** weak references = missed steps. Claude needs explicit, imperative pointers.
- **Con:** more files to maintain; path refactors break references.

## Open questions / gotchas
_(empty — will fill as we discuss)_
