---
description: Prompt-Dimensionen bewerten bevor Claude antwortet
argument-hint: "[prompt]"
allowed-tools: ["AskUserQuestion"]
---

# Prompt Refiner

Schnelle Dimension-Bewertung vor der Antwort. Tinder-Prinzip: eine Dimension, ein Tastendruck, weiter.

## Ablauf

### 1. Prompt bestimmen

Mit Argument (`/refine Bau mir eine Login-Seite`): verwende das Argument.
Ohne Argument: frage den User.

### 2. Dimensionen identifizieren

Analysiere den Prompt. Identifiziere **genau 4** Dimensionen, in denen der Prompt vage ist. Jede Dimension = eine offene Designentscheidung.

Pro Dimension:
- **Name**: 1-2 Worte, max 12 Zeichen (z.B. "Auth", "Styling", "Security", "Errors")
- **Hint**: kurzer Trade-off (z.B. "Social Login vs Passwort")

Wenn der Prompt bereits spezifisch genug ist, ueberspringe die Bewertung und bearbeite ihn direkt.

### 3. Bewerten lassen

Ein einziger AskUserQuestion-Call mit allen 4 Dimensionen. Format:

```json
{
  "questions": [
    {
      "question": "[Name] — [Hint]",
      "header": "[Name]",
      "multiSelect": false,
      "options": [
        {"label": "nicht relevant", "description": "Kein Aufwand"},
        {"label": "egal", "description": "AI entscheidet"},
        {"label": "relevant", "description": "Sorgfaeltig umsetzen"},
        {"label": "besonders wichtig", "description": "Top-Prioritaet"}
      ]
    }
  ]
}
```

WICHTIG: Die Descriptions sind immer identisch (Kein Aufwand / AI entscheidet / Sorgfaeltig umsetzen / Top-Prioritaet). Der Hint steht NUR in der Frage, NICHT in den Descriptions. So ist jede Option auf einen Blick unterscheidbar.

Die 4 Stufen der Skala:
1. **nicht relevant** = Leitplanke. "Investiere hier nichts."
2. **egal** = Freiheit. "AI darf frei entscheiden." Die wichtigste Option.
3. **relevant** = Fokus. "Handle das sorgfaeltig."
4. **besonders wichtig** = Top-Prioritaet. "Maximaler Aufwand."

### 4. Enrichment anwenden

Wende die Bewertungen auf deine Antwort an:

- **besonders wichtig**: Top-Prioritaet. Maximaler Aufwand, produktionsreife Qualitaet. Bekommt den meisten Raum in der Antwort.
- **relevant**: Sorgfaeltig und durchdacht umsetzen.
- **egal**: AI hat volle kreative Freiheit. Nutze dein bestes Urteil — das ist kein "unwichtig", sondern "du darfst entscheiden".
- **nicht relevant**: Leitplanke. Investiere hier keinen Aufwand. Uebergehe diesen Aspekt oder halte ihn minimal.

### 5. Antworten

Bearbeite den urspruenglichen Prompt. Erwaehne die Bewertung NICHT — lass sie unsichtbar dein Verhalten steuern.
