# Prompt Refiner

Rate what matters before Claude responds. 4 dimensions, 4 keystrokes, better output.

## Install

```
/plugin marketplace add Heinrichs-Heinrichs/prompt-refiner
/plugin install prompt-refiner@prompt-refiner
```

## Command

### `/refine`

Identifies ambiguous dimensions in your prompt and lets you rate their importance before Claude responds.

**Usage:**

```
/refine <your prompt>
```

**Example:**

```
> /refine give me a lemon muffin recipe

  ┌ Effort   Glaze   Texture   Lemon   Submit ┐

  Effort — Simple vs. elaborate?
  1. not relevant      Skip
  2. don't care        AI decides        ← you pick this
  3. relevant          Handle carefully
  4. very important    Top priority

  Glaze — Drizzle vs. proper icing?
  4. very important    Top priority      ← you pick this

  Texture — Dense vs. fluffy?
  3. relevant          Handle carefully  ← you pick this

  Lemon — Subtle vs. intense?
  4. very important    Top priority      ← you pick this
```

**Without /refine** — basic recipe, 7 steps, glaze is "optional":

```
Zutaten:
- 250 g Mehl, 150 g Zucker, 2 Eier, 120 ml Öl ...

Zubereitung:
1. Ofen auf 180 °C vorheizen.
2. Trockene Zutaten mischen.
...
7. Optional mit Zitronenglasur beträufeln.
```

**With /refine** — same prompt, after rating Glaze and Lemon as "very important":

```
Zutaten:
  Teig: 250 g Mehl, 150 g Zucker, 120 ml Buttermilch,
        Saft + Abrieb von 2 Bio-Zitronen, 1 TL Vanilleextrakt ...
  Zitronen-Glasur: 150 g Puderzucker, Zitronensaft,
        Abrieb von 1 Bio-Zitrone, 1 Prise Fleur de Sel
  Streusel-Topping: 60 g Mehl, 40 g kalte Butter,
        1 EL Zitronenzeste, 1 Prise Fleur de Sel

Zubereitung:
  Streusel vorbereiten:
    Mehl, Zucker und Zeste mischen. Kalte Butter einarbeiten ...
  Teig:
    1. Nur kurz verrühren — ein paar Klumpen sind ok.
    ...
  Glasur:
    Puderzucker sieben, Zitronensaft löffelweise einrühren ...
    Über die lauwarmen Muffins träufeln — so zieht sie ein
    und bildet trotzdem eine glatte Oberfläche.

Tipps:
- Zeste immer mit feiner Microplane reiben
- Glasur erst kurz vor dem Servieren, wenn sie knackig bleiben soll
```

The dimensions you rated as important got depth. The ones you didn't care about stayed lean.

## The Scale

| Key | Level | What it tells Claude |
|-----|-------|---------------------|
| 1 | not relevant | Guardrail — skip this entirely |
| 2 | don't care | Freedom — AI decides (this is the most useful option) |
| 3 | relevant | Handle with care |
| 4 | very important | Top priority — maximum effort |

## How It Works

1. You type `/refine <prompt>`
2. Claude identifies 4 ambiguous dimensions in your prompt
3. You rate each with a single keypress (1-4)
4. Claude responds with your priorities baked in — without mentioning them

No API keys. No dependencies. The entire plugin is one markdown file that uses Claude's built-in `AskUserQuestion` tool.

## License

MIT — [Heinrichs & Heinrichs](https://github.com/Heinrichs-Heinrichs)
