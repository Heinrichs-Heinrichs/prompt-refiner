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
/refine give me a lemon muffin recipe
```

Claude shows 4 dimensions. You rate each with a single keypress:

```
  ┌ Effort   Glaze   Texture   Lemon   Submit ┐

  Effort — Simple vs. elaborate?
  1. not relevant      Skip
  2. don't care        AI decides        ← you pick this
  3. relevant          Handle carefully
  4. very important    Top priority
```

**Without /refine:**

```
Lemon Muffins (12 pieces)

Ingredients:
- 250 g flour, 150 g sugar, 2 tsp baking powder, ¼ tsp salt,
  2 eggs, 120 ml oil, 125 ml milk, zest of 2 lemons, 3 tbsp lemon juice

Glaze (optional):
- 100 g powdered sugar, 2-3 tbsp lemon juice

Instructions:
1. Preheat oven to 180 °C, line muffin tin.
2. Mix dry ingredients.
3. Whisk wet ingredients.
4. Combine — stir briefly, batter can be lumpy.
5. Divide into 12 cups.
6. Bake 20-25 min (toothpick test).
7. Cool, optionally drizzle with glaze.
```

**With /refine** — after rating Glaze and Lemon as "very important":

```
Lemon Muffins (12 pieces)

Ingredients:
  Batter: 250 g flour, 150 g sugar, 2 tsp baking powder, ¼ tsp salt,
    2 eggs, 120 ml buttermilk, 80 ml neutral oil,
    juice of 2 lemons (~80 ml), zest of 2 organic lemons, 1 tsp vanilla

  Lemon Glaze: 150 g powdered sugar, 2-3 tbsp fresh lemon juice,
    zest of 1 organic lemon, 1 pinch fleur de sel

  Streusel Topping: 60 g flour, 40 g cold butter (cubed),
    30 g sugar, 1 tbsp lemon zest, 1 pinch fleur de sel

Instructions:
  Streusel:
    Mix flour, sugar and zest. Work in cold butter until coarse
    crumbs form. Mix in fleur de sel. Refrigerate.

  Batter:
    1. Preheat to 190 °C. Line muffin tin.
    2. Combine dry ingredients.
    3. Whisk wet ingredients with lemon juice, zest and vanilla.
    4. Fold wet into dry. Stir briefly — a few lumps are fine.
       Overmixing makes muffins tough.
    5. Fill cups ¾ full. Scatter streusel on top.

  Baking:
    18-22 min at 190 °C. Toothpick test. Cool 10 min in tin,
    then transfer to wire rack.

  Glaze:
    Sift powdered sugar. Stir in lemon juice one spoonful at a time
    until thick but pourable. Mix in zest and salt. Drizzle over
    lukewarm muffins — it soaks in and forms a smooth surface.

Tips:
- The streusel + glaze combo gives two textures: crunchy and smooth-sweet
- Always use a fine microplane for zest — only the yellow layer, never the
  white pith
- Keep airtight for 3 days. Add glaze just before serving for crunch.
```

Same prompt. 4 keystrokes. The dimensions you cared about got depth.

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
