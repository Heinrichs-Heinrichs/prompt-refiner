# Prompt Refiner

Ping-pong your way to a precise answer. Quick questions, zero effort, better output.

## Install

```
/plugin marketplace add Heinrichs-Heinrichs/prompt-refiner
/plugin install prompt-refiner@prompt-refiner
```

## Command

### `/prompt-refiner:ask`

Asks quick multiple-choice questions to understand your intent before Claude responds. Like the Akinator game — but for prompts.

**Usage:**

```
/prompt-refiner:ask <your prompt>
```

**Example:**

```
/prompt-refiner:ask write an email to my boss
```

Claude starts a ping-pong:

```
Round 1:  "What's it about?"
          → Raise | Time off | Resignation | don't care

You: Raise

Round 2:  "What tone?" + "Mention a specific number?"
          → Confident | Diplomatic | don't care
          → Yes, name a figure | No, request a meeting first | don't care

You: Diplomatic, Request a meeting

Round 3:  "How detailed?"
          → Short & direct | Thorough with reasoning | don't care

You: Thorough with reasoning

Claude: [enough clarity] → writes the email
```

3 rounds. A few clicks. The answer matches exactly what you had in mind.

**Without `/prompt-refiner:ask`:**

```
Subject: Meeting Request

Dear [Boss],

I would like to schedule a meeting to discuss my current
compensation. Please let me know a convenient time.

Best regards
```

**With `/prompt-refiner:ask`** — after clarifying tone, detail level, and approach:

```
Subject: Request for a Compensation Discussion

Dear [Boss],

Over the past year, I've taken on several responsibilities beyond
my original role — including leading the Q3 migration project and
mentoring two junior developers on the team.

I'm proud of what we've accomplished, and I'd welcome the
opportunity to sit down and discuss how my compensation might
reflect these contributions going forward.

Would any time next week work for a 20-minute conversation?
I'm flexible and happy to adjust to your schedule.

Best regards
```

Same prompt. A few clicks. The answer has depth where it matters.

## How It Works

1. You type `/prompt-refiner:ask <prompt>`
2. Claude asks short multiple-choice questions (1-4 per round)
3. You pick answers — every question has a "don't care" option
4. Claude stops when it has enough clarity
5. Claude responds with your intent baked in — without mentioning the questions

**Every question has a "don't care / AI decides" option.** You never have to have an opinion. Skip what you don't care about, focus on what matters.

## Question Types

| Type | When | Example |
|------|------|---------|
| Choices | Real alternatives exist | "Which DB?" → Postgres / Mongo / don't care |
| Scale | It's about effort/depth | "How important is error handling?" → skip / don't care / careful / top priority |
| Binary | Only two directions | "With or without tests?" → With / Without / don't care |

## License

MIT — [Heinrichs & Heinrichs](https://github.com/Heinrichs-Heinrichs)
