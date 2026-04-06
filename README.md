# Prompt Refiner

4 clicks instead of 40 words. Same result.

## Install

```
/plugin marketplace add Heinrichs-Heinrichs/prompt-refiner
/plugin install prompt-refiner@prompt-refiner
```

## The Idea

You know what you want. You just don't want to type it all out.

Instead of crafting the perfect prompt, answer a few quick multiple-choice questions. Claude narrows down your intent through elimination — like Akinator, but for prompts. Each round builds on the last, getting closer to exactly what you mean.

## Example

```
/prompt-refiner:ask plan a trip
```

```
Round 1:  "What kind of trip?"
          → Beach & relax | City & culture | Active & adventure | don't care

You: Active & adventure

Round 2:  "How long?" + "Traveling with?"
          → Weekend | ~5 days | 2+ weeks | don't care
          → Solo | With partner | Group of friends | don't care

You: ~5 days, With partner

Round 3:  "Budget per person?"
          → Budget (<€500) | Mid-range | Splurge | don't care

You: Mid-range
```

Claude now has the same clarity as if you had typed:

```
Plan a 5-day adventure trip for two, mid-range budget,
active outdoor activities over sightseeing, somewhere in
Europe reachable by train, no resort vibes, we like hiking
and local food
```

**3 rounds. 4 clicks. Zero typing.**

You didn't have to formulate any of that. You just picked options.

## How It Works

1. You type `/prompt-refiner:ask <prompt>`
2. Claude asks 1-4 multiple-choice questions per round
3. You click — every question has a "don't care" option
4. Each round builds on your previous answers (narrowing down, not repeating)
5. Claude stops when it has enough clarity and responds

**Every question has a "don't care / AI decides" option.** You never have to have an opinion. Skip what you don't care about, focus on what matters to you.

## Why Not Just Ask Claude Directly?

You can. But then Claude either:
- **Answers immediately** — generic, because it guessed your intent
- **Asks back in free text** — now you're typing paragraphs to answer its questions

This plugin gives you the precision of a detailed prompt with the effort of a few clicks. The questions are multiple-choice, they build on each other, and you can skip any you don't care about.

## License

MIT — [Heinrichs & Heinrichs](https://github.com/Heinrichs-Heinrichs)
