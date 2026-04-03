# Prompt Refiner

> You know what you want. You just don't type it all out. This plugin bridges the gap.

A [Claude Code](https://claude.ai/claude-code) plugin that turns vague prompts into prioritized ones — with 4 keystrokes.

## Why

Every prompt you write is incomplete. You have a detailed picture in your head, but you type a sentence. Claude fills the gaps with assumptions. Sometimes it nails it. Often it doesn't. You iterate, re-prompt, get frustrated.

You *could* write more context upfront. But you won't — because the effort doesn't feel worth it until you see the mediocre output.

Prompt Refiner fixes this with a Tinder-like interaction: before Claude responds, it shows you 4 dimensions where your prompt is ambiguous. You rate each one with a single keypress. Done.

## Before & After

```
/refine give me a lemon muffin recipe
```

Claude identifies 4 ambiguous dimensions — you rate each instantly:

| Dimension | Your rating |
|-----------|------------|
| Effort | don't care |
| Glaze | **very important** |
| Texture | relevant |
| Lemon Intensity | **very important** |

**Without /refine** you get a basic 7-step recipe where glaze is an afterthought ("optional: drizzle with powdered sugar").

**With /refine** you get streusel topping with lemon zest and fleur de sel, a proper glaze section with technique ("drizzle over lukewarm muffins — it soaks in and forms a smooth surface"), texture tips ("fold gently, a few lumps are fine"), and microplane advice for the zest. The dimensions you cared about got real depth. The ones you didn't care about stayed lean.

Same prompt. 4 keystrokes. ~5 seconds. Completely different result.

## The Scale

```
1  not relevant     "Don't bother with this."
2  don't care       "AI decides — I trust you."
3  relevant         "Handle this carefully."
4  very important   "This is what I care about most."
```

**"Don't care" is the most powerful option.** It's not "unimportant" — it's explicit permission. You're telling Claude: *use your best judgment here, I won't second-guess you.* That signal is just as valuable as "very important".

## Install

In Claude Code:

```
/plugin marketplace add Heinrichs-Heinrichs/prompt-refiner
/plugin install prompt-refiner@prompt-refiner
```

## Usage

```
/refine <your prompt>
```

That's it. Claude analyzes your prompt, shows 4 dimensions, you press 1-4 for each, and the response reflects your priorities. The ratings are applied invisibly — you won't see them mentioned in the output.

Works with any kind of prompt: code, writing, recipes, architecture decisions, design briefs.

## Under the Hood

No API keys. No external dependencies. No background processes.

The entire plugin is a single markdown file that instructs Claude how to use its built-in `AskUserQuestion` tool. When you type `/refine`, Claude reads the instruction, identifies ambiguous dimensions in your prompt, asks you to rate them, and adjusts its response accordingly.

## License

MIT — [Heinrichs & Heinrichs](https://github.com/Heinrichs-Heinrichs)
