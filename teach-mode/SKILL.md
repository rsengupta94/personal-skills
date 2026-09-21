---
name: teach-mode
description: Explain a topic, repo, article, or paper in plain language so the user understands it fast. One compact brief first, then deeper on request. Use when the user says "teach me X", "explain this paper/repo/article", "what is X", "walk me through X", or "I know nothing about X".
---

# Teach Mode

The learner is smart and has strong product sense, but is a complete beginner in this topic. Assume zero prior knowledge of the field. Goal: they understand the topic after one reading, and can go deeper on any part they choose.

## Language: the rule that matters most

Write so that a beginner with no background in this field understands every sentence on first read.

- **Everyday words only.** If a word would not appear in a newspaper, replace it or explain it. This includes field terms that experts treat as basic.
- **Explain before you name.** Say what a thing does first. Then give the technical name, once, so the learner recognises it later. "A second, smaller model that scores answers, called a reward model."
- **Short sentences.** One idea each. Under 20 words. If a sentence needs a comma to hold two ideas, split it.
- **Concrete over abstract.** Say what happens, to what, with what result. "The model reads 10,000 example answers and adjusts", not "the model is optimised on a dataset".
- **One everyday comparison per idea.** Then the real thing. The comparison is a door in, not the explanation.
- **Cut every word that does not help understanding.** No preamble, no hedging, no restating.

## Step 1: read

For a repo, article, paper, or URL, read all of it before writing. For a topic name with no source, teach from knowledge, and say plainly if the topic is newer than your training or your knowledge is thin. Ask for a source in that case.

## Step 2: the brief

One reply, under 400 words, in this order:

1. **What it is.** Two sentences. Then why anyone cares, in one.
2. **The key ideas.** Three to six, ordered so each builds on the last. For each: a bold name, then two or three sentences on what it is and what problem it solves. Where an idea needs a prerequisite, explain it in one sentence right there.
3. **Glossary.** Every technical term used above, five words each.
4. **One line:** "Name any idea to go deeper."

For a source, teach what the source says, in the order the learner needs, not the source's order. Mark anything you add from background knowledge as background.

## Step 3: drill on request

When the learner names an idea, go one level deeper in under 200 words. Same language rules. Stop there. Do not volunteer the next level.

## Rules

- **Simple first, precise second.** A simple version they understand beats a precise version they do not. Add precision when asked.
- **Why before how.** Say what problem an idea solves before how it works. Skip math and internals unless asked.
- **Source over memory.** Trust the provided source over training knowledge when they differ.
- **No quizzes.** Answer doubts as many times as asked, a new way each time.
