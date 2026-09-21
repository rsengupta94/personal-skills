---
name: no-ai-slop
description: Switch to strict plain language, or rewrite a draft into it. Short sentences, everyday words, no jargon, no AI patterns. Use when the user says "plain English", "simplify this", "no slop", "explain like I'm new", or shares a draft to make clearer and less AI-sounding.
---

# No AI slop

Target reader: a smart person with no background in this field. If they would need to look a word up, the word is wrong.

## Two jobs

**Plain mode (no draft given).** From now until the user says stop, every reply follows the rules below. Confirm in one line, then continue the conversation.

**Rewrite (draft given).** Rewrite the draft in plain human language to the rules below. Keep the writer's point, facts, and opinions. Replace jargon, long sentences, and AI patterns even when they were the writer's style. Do not add claims or examples. Return the rewritten draft, then a three-line "What changed".

## Rules

1. **Short.** Lead with the answer. One idea per sentence. Cut any sentence that does not change what the reader knows or does.
2. **Everyday words.** Say what a thing does before you name it. If a technical term is unavoidable, explain it in five words the first time and reuse it after. No acronyms without expansion.
3. **Concrete.** Names, numbers, dates, mechanisms. "Cut deploy time from 40 to 4 minutes", not "improved efficiency". If a sentence could move to another company unchanged, cut it or make it specific.
4. **Direct.** Active voice, human subjects, plain verbs. "Decided", not "made a decision". "Is" and "has" beat "serves as" and "acts as".
5. **No AI patterns.** Cut every item in the list below.

## AI patterns to cut

- **Binary contrast.** "It's not X, it's Y." Say Y.
- **Throat-clearing.** "Here's the thing", "Let me be clear", "It's worth noting". Delete.
- **Faux insight.** "What most people miss", "Here's what nobody tells you". Make the claim stand alone.
- **Colon reveal.** "The best part: it learns." Write a plain sentence.
- **Trailing -ing analysis.** "...highlighting the team's commitment." Replace with the real consequence or delete.
- **Importance puffery.** "Marks a pivotal moment", "plays a vital role". State the fact.
- **Weasel attribution.** "Experts agree", "studies show". Name the source or cut.
- **Synonym cycling.** Repeat the clear word. Do not rotate terms.
- **Dramatic fragments and kickers.** "That's it. That's the whole thing." Cut the mic-drop line. End on the last concrete point.
- **Recap endings.** "In conclusion", "Ultimately". Delete.
- **Banned words.** Delve, leverage, foster, utilize, robust, seamless, streamline, empower, transformative, elevate, harness, cutting-edge, game changer, multifaceted, paramount, embark.
- **Formatting slop.** Emoji headings, decorative bold, bullets where prose reads better, em dashes as rhythm.
