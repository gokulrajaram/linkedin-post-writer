# linkedin-post-writer

A [Claude Code](https://claude.com/claude-code) and Codex skill for drafting long-form LinkedIn posts in the voice of a seasoned operator/investor, aimed at an audience of startup founders and tech CEOs.

This is an opinionated skill. It enforces a specific structure (hook → setup → analysis → framework → declarative CTA), bans common AI tells (em-dashes as punctuation, negative parallelism like "it's not X, it's Y", "think about…" openers, trailing questions), and always runs a humanizer pass before returning the draft.

## Install

Copy the skill into your Claude Code skills directory:

```bash
git clone https://github.com/<your-username>/linkedin-post-writer.git
mkdir -p ~/.claude/skills
cp -r linkedin-post-writer ~/.claude/skills/
```

Then in Claude Code, invoke it with `/linkedin-post-writer` followed by a topic, anecdote, or rough thought. For example:

```
/linkedin-post-writer write a post about why founders should stay in role longer than 2 years
```

Or just describe what you want in plain English — the skill will trigger automatically when your request looks like a LinkedIn draft.

## What's in the skill

- **`SKILL.md`** — the prompt. Defines the voice, the five-part post structure, the hard constraints, and the drafting workflow.
- **`references/voice-samples.md`** — four prior posts that anchor the target voice. Loaded on demand when the model needs to calibrate.
- **`evals/evals.json`** — eval cases used while iterating on the skill.

## Customizing the voice

The four samples in `references/voice-samples.md` are the single biggest lever for tuning the output to sound like *you*. Replace them with 3–5 of your own posts that represent the voice you want, and the skill will recalibrate.

Keep the structural rules (hook, framework, declarative CTA) intact unless you want to change the form of the posts, not just the voice.

## Hard rules the skill enforces

These live in `SKILL.md` and are the main reason the output avoids the usual AI-generated LinkedIn sludge:

1. Never end with a question. Close declaratively.
2. No em-dashes or en-dashes as punctuation — colons instead.
3. No "it's not X, it's Y" / negative parallelism. State what IS directly.
4. No "Think about…" / "Consider…" / "Imagine…" openers.
5. No invented public-figure examples. If the user didn't supply an anchor, build from first principles.
6. Always run the `humanizer` pass (or its rules from memory) before returning.

## License

MIT. See [LICENSE](LICENSE).
