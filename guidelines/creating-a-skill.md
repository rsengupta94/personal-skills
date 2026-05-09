# Creating a Skill — End-to-End Process

The operational playbook for creating a Claude Code skill from scratch — for me to follow, and for Claude to follow on my behalf.

For *concepts* (what a skill is, how `SKILL.md` is structured, description best practices, body principles, bundled files), see `learning.md`. This doc is the workflow.

---

## Step 0 — Should this be a skill at all?

Run the 3-question gate (see `learning.md` → "Mental shortcut"):

1. **Repeatable** — will I want this same behavior again?
2. **Non-trivial** — multi-step, opinionated, or easy to misremember?
3. **Bounded** — clearly applicable only sometimes (not always-on)?

**If any answer is "no", do not make a skill.** Use a one-off prompt, a `CLAUDE.md` rule, a slash command, or a tool instead.

Sanity check: *"Have I done this same thing more than twice in the last month?"*

---

## Step 1 — Brief Claude

Open a Claude Code session. Give Claude these inputs:

| Input | What to provide |
|---|---|
| **Problem** | The failure mode this skill should fix. |
| **Past instances** | 2–3 real moments when I'd have wanted this. Actual prompts, actual situations. |
| **Trigger phrases** | Phrasing I'd naturally use to invoke it. |
| **Desired behavior** | What Claude should *do*. Walk through the steps in my own words. |
| **Constraints** | Things Claude must NOT do (guardrails). |
| **Family** | Behavior shift / workflow / artifact (see `learning.md` → "What skills can do"). |
| **Bundled files?** | Templates, references, scripts? Or single `SKILL.md`? |
| **Spec reference** | Point Claude at `learning.md` for the description and body principles. |

### Briefing prompt template

> Help me write a skill called `<name>`. The problem it solves is [...]. Here are 3 past situations where I wanted it: [...]. I'd typically trigger it by saying [phrases]. The behavior I want is [walk through]. It must not [constraints]. I think this is a [family] skill. Use the description and body principles from `learning.md`.

---

## Step 2 — Review Claude's draft (the smell list)

Claude has predictable failure modes when authoring skills. Read its draft and push back on:

| Smell | Push-back |
|---|---|
| Description is pure WHAT, no WHEN | "Add explicit trigger phrases — both intent-based and literal." |
| Documentation prose ("This skill helps...") | "Rewrite the body in imperative voice. Drop the preamble." |
| Vague verbs ("consider", "be mindful of") | "Replace with concrete actions." |
| Bloated body (>150 lines) | "Strip what Claude already knows. Push detail into bundled files if needed." |
| No gates between phases | "Add stop conditions: 'Do not proceed until X.'" |
| Premature bundled files | "Inline this back into SKILL.md until the body crosses ~150 lines." |
| Restating the description in the body | "Cut. Already in context." |

Iterate with Claude until the draft passes these smells.

For deeper guidance on what makes a strong description and body, see `learning.md` → "How to build a skill".

---

## Step 3 — Decide the scope (where it lives)

| Question | Scope | Path |
|---|---|---|
| Personal, used everywhere? | **User** | `~/.claude/skills/<name>/SKILL.md` |
| Specific to one codebase? | **Project** | `<project>/.claude/skills/<name>/SKILL.md` |
| For my team to share? | **Project (committed)** | `<project>/.claude/skills/<name>/SKILL.md` |
| For public sharing? | **Plugin** | published via plugin tooling |

Default for personal skills: **user scope**.

---

## Step 4 — Place the skill

```bash
# User scope (most common for personal skills)
mkdir -p ~/.claude/skills/<name>
# Save SKILL.md (and any bundled files) inside

# Project scope
mkdir -p <project-root>/.claude/skills/<name>
# Save SKILL.md (and any bundled files) inside
```

Folder name should match the skill's `name` field. No registration step — filesystem placement is the entire installation.

---

## Step 5 — Validate (the 3 tests)

**Start a fresh Claude Code session before testing.** Mid-session edits aren't reliably picked up — the menu is built once at session start.

### Test 1 — Explicit invocation
Type `/<name>` and walk through intended use. Watch:
- Does Claude follow the body in order?
- Does it respect the gates?
- Does it load bundled files when referenced?
- Does the output match expectations?

Failures here → sharpen the **body**.

### Test 2 — Auto-invocation
In a fresh session, paraphrase a real trigger in natural language — don't type `/<name>`.
- Auto-fired correctly → description is matching well.
- Didn't fire → description is invisible. Sharpen trigger phrases.
- Fired when not wanted → description is too broad. Tighten it.

Failures here → sharpen the **description**.

### Test 3 — Failure modes
Throw deliberately weird inputs: incomplete info, contradictory signals, ambiguous prompts. Does the skill follow its escape hatches? Does it ask for clarification when it should?

Failures here → add explicit failure-mode handling to the **body**.

---

## Step 6 — Iterate

**A first-draft skill is a hypothesis, not a product.** Plan for 3–5 iterations on any non-trivial skill.

Loop:
1. Use the skill on real work.
2. Note where Claude's behavior deviated from intent.
3. The deviation tells you exactly what's missing in the body or description.
4. Edit `SKILL.md`. Reload. Test again.

Skills used 20 times are 5× better than skills written once and put away.

---

## Step 7 — Maintain

Three habits keep the catalog from rotting:

- **Prune** — quarterly, review which skills I actually used. Delete the ones that didn't earn keep. A bloated catalog dilutes auto-invocation matching.
- **Version** — keep skills under git (see Step 8).
- **Watch for description collisions** — if two skills' descriptions overlap, Claude gets confused about which to invoke. Rewrite or merge.

---

## Step 8 — Cross-machine sync (when the catalog is worth keeping in sync)

User skills live in `~/.claude/skills/`, which is per-machine. To use them on multiple machines:

```bash
# Setup on the first machine
mkdir ~/skills && cd ~/skills && git init

# Move existing skill folders into the repo
mv ~/.claude/skills/* ~/skills/

# Symlink each skill folder back to where Claude Code looks
mkdir -p ~/.claude/skills
for skill in ~/skills/*/; do
  ln -s "$skill" ~/.claude/skills/
done

git add . && git commit -m "initial skills" && git push

# On a new machine
git clone <repo-url> ~/skills
mkdir -p ~/.claude/skills
for skill in ~/skills/*/; do ln -s "$skill" ~/.claude/skills/; done
```

Now skills are versioned, portable, and editable from either path.

---

## Full flow at a glance

```
Step 0: Run the 3-question gate. Skip if any "no".
Step 1: Brief Claude using the template above.
Step 2: Review Claude's draft against the smell list.
Step 3: Decide scope (user / project / plugin).
Step 4: Place the skill at the right path.
Step 5: Validate with 3 tests (explicit / auto / failure-mode).
Step 6: Iterate — skills are tuned, not authored.
Step 7: Maintain (prune, version, collisions).
Step 8: Sync across machines via dotfiles/git when worth it.
```
