# Prompt Refiner

A Claude Code plugin that adds a `/refine` command for quick prompt disambiguation. Before Claude responds, you rate 4 key dimensions with a single keypress each — turning vague prompts into focused, prioritized ones.

## The Problem

Every AI prompt is a compromise. You have a picture in your head but type only a fraction of it. The AI fills the gaps with assumptions — and often gets it wrong.

The bottleneck isn't AI quality, it's context loss between your head and the input field. You *could* specify more, but you don't — because the effort only shows in the bad output.

## The Solution

Instead of typing more context, you **rate dimensions**. The plugin identifies what's ambiguous in your prompt and presents 4 key decision points. You press 1-4 for each, and Claude knows your priorities.

**4 keystrokes. ~5 seconds. Done.**

## Example

**Without** `/refine` — "give me a lemon muffin recipe":

> Basic recipe, 7 steps, glaze listed as "optional". Gets the job done, nothing more.

**With** `/refine` — same prompt, 4 keypresses:

```
/refine give me a lemon muffin recipe
```

Claude identifies 4 dimensions. You rate each with a single keypress:

```
  Effort     Glaze    Texture   Lemon
  ─────────────────────────────────────
  1. not relevant       Skip
  2. don't care         AI decides
  3. relevant           Handle carefully
  4. very important     Top priority
```

Say you rate: Effort → don't care, Glaze → very important, Texture → relevant, Lemon → very important.

The result: a recipe with lemon streusel topping, a detailed glaze section (powdered sugar, zest, fleur de sel), tips on texture ("fold gently — a few lumps are fine"), microplane advice for the zest, and storage instructions. The dimensions you rated as important got real depth.

**Same prompt. 4 keystrokes. Dramatically different output.**

## The Scale

| Key | Level | Meaning |
|-----|-------|---------|
| 1 | not relevant | Guardrail — don't invest effort here |
| 2 | don't care | Freedom — AI decides (the most important option) |
| 3 | relevant | Handle carefully |
| 4 | very important | Top priority — maximum effort |

"Don't care" is the most powerful option. It tells the AI: *I trust your judgment here.* That's not "unimportant" — it's explicit permission to be creative.

## Install

```
/plugin marketplace add Heinrichs-Heinrichs/prompt-refiner
/plugin install prompt-refiner@prompt-refiner
```

## Usage

```
/refine Build me a login page
```

Claude identifies 4 ambiguous dimensions (e.g. Auth, Styling, Security, Errors), you rate each with a single keypress, and Claude responds with your priorities in mind.

## How It Works

1. You type `/refine <your prompt>`
2. Claude analyzes the prompt and identifies 4 vague dimensions
3. You see each dimension as a question — press 1-4 to rate
4. Claude applies your ratings invisibly to its response

No API keys needed. No external dependencies. Just one markdown file that tells Claude how to use its native `AskUserQuestion` tool.

## License

MIT
