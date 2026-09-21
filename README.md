# personal-skills

A set of reusable instruction files for Claude Code, the command-line coding assistant from Anthropic. Each file tells Claude how to handle one kind of task. Examples: writing a README, or rewriting a draft in plain English. Written for one person's own use and shared for anyone who wants to copy or adapt them.

## What is in the repo

A skill is a folder holding one `SKILL.md` file. Claude reads the file only when you call the skill by name or when your request matches its description.

| Folder | What Claude does when it runs |
|---|---|
| `brainstorm-mode/` | Acts as a blunt sparring partner for product brainstorming. One question or position per turn. Redirects away from implementation talk. |
| `no-ai-slop/` | Writes in strict plain language, or rewrites a draft into it. Short sentences, everyday words, no AI writing patterns. |
| `second-pass/` | Checks a finished plan, spec, or decision for gaps before you rely on it. Proposes only small, evidence-backed edits. |
| `teach-mode/` | Explains a topic, repo, article, or paper in plain language for a beginner. One short brief first, then deeper on request. |
| `write-readme/` | Writes or updates a repo README. Every install and run step is checked against the repo's real files. |

## How to use

You need Claude Code installed. Claude Code looks for personal skills in the `~/.claude/skills/` folder on your machine.

Clone the repo:

```bash
git clone https://github.com/rsengupta94/personal-skills.git ~/skills
```

This downloads the repo into a folder named `skills` in your home directory.

Link each skill folder into the place Claude Code reads from:

```bash
mkdir -p ~/.claude/skills
for skill in ~/skills/*/; do ln -s "$skill" ~/.claude/skills/; done
```

This creates a shortcut for every skill folder. Editing a file in `~/skills` also changes what Claude reads.

Start a new Claude Code session. Skills are read once at session start, so an open session will not see them.

Call a skill by typing a slash and its folder name, for example:

```
/write-readme for this repo
```

Claude will follow the steps in that skill's file. You can also describe the task in plain words. Claude picks the skill when your request matches its description.

To install one skill only, copy its folder instead of linking everything:

```bash
mkdir -p ~/.claude/skills
cp -r ~/skills/no-ai-slop ~/.claude/skills/
```

## Status and license

These skills are in active use and change often. The repo has no license file yet.
