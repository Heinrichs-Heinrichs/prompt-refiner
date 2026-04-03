# Prompt Refiner

A Claude Code plugin that adds a `/refine` command for quick prompt disambiguation. Before Claude responds, you rate 4 key dimensions with a single keypress each — turning vague prompts into focused, prioritized ones.

## The Problem

Every AI prompt is a compromise. You have a picture in your head but type only a fraction of it. The AI fills the gaps with assumptions — and often gets it wrong.

The bottleneck isn't AI quality, it's context loss between your head and the input field. You *could* specify more, but you don't — because the effort only shows in the bad output.

## The Solution

Instead of typing more context, you **rate dimensions**. The plugin identifies what's ambiguous in your prompt and presents 4 key decision points. You press 1-4 for each, and Claude knows your priorities.

**4 keystrokes. ~5 seconds. Done.**

The scale:

| Key | Level | Meaning |
|-----|-------|---------|
| 1 | nicht relevant | Guardrail — don't invest effort here |
| 2 | egal | Freedom — AI decides freely |
| 3 | relevant | Handle carefully |
| 4 | besonders wichtig | Top priority — maximum effort |

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

No API keys needed. No external dependencies. Just one markdown file that tells Claude how to use `AskUserQuestion`.

## License

MIT
