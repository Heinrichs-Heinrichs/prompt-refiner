---
description: Akinator-Style Ping-Pong — klaert deine Intention bevor Claude antwortet
argument-hint: "[prompt]"
allowed-tools: ["AskUserQuestion"]
---

# Akinator

Iterativer Ping-Pong-Flow: Stelle kurze MC-Fragen, um die User-Intention zu verstehen. Antworte erst, wenn genug Klarheit herrscht. Ziel ist nicht den Prompt zu verfeinern, sondern die Antwort praeziser zu machen.

## Ablauf

### 1. Prompt bestimmen

Mit Argument (`/akinator Bau mir eine Login-Seite`): verwende das Argument.
Ohne Argument: frage den User.

### 2. Analyse

Analysiere den Prompt. Identifiziere intern, welche Aspekte ambig sind — wo koennte die Antwort in verschiedene Richtungen gehen?

Wenn der Prompt bereits spezifisch genug ist: keine Fragen, direkt antworten.

### 3. Ping-Pong-Loop

Starte den iterativen Fragenloop. Pro Runde:

**a) Intern bewerten**: Welche Aspekte haben die groesste Unklarheit? Wo wuerde eine Klaerung den groessten Einfluss auf die Qualitaet der Antwort haben?

**b) Fragen formulieren**: 1-4 MC-Fragen pro Runde via AskUserQuestion. Buendle unabhaengige Fragen, stelle abhaengige Fragen seriell in der naechsten Runde.

**c) Fragentyp waehlen**: Du hast drei Typen zur Verfuegung. Waehle pro Frage den passenden:

**Typ A — Inhaltliche Optionen** (wenn es echte Alternativen gibt):

```json
{
  "question": "Welche Datenbank?",
  "header": "DB",
  "multiSelect": false,
  "options": [
    {"label": "PostgreSQL", "description": "Relational, bewaehrt"},
    {"label": "MongoDB", "description": "Document-basiert, flexibel"},
    {"label": "egal", "description": "AI entscheidet"}
  ]
}
```

**Typ B — Wichtigkeits-Skala** (wenn es um Aufwand/Tiefe geht):

```json
{
  "question": "Wie wichtig ist Error Handling?",
  "header": "Errors",
  "multiSelect": false,
  "options": [
    {"label": "nicht relevant", "description": "Kein Aufwand"},
    {"label": "egal", "description": "AI entscheidet"},
    {"label": "relevant", "description": "Sorgfaeltig umsetzen"},
    {"label": "besonders wichtig", "description": "Top-Prioritaet"}
  ]
}
```

**Typ C — Binaere Entscheidung** (wenn es nur zwei Richtungen gibt):

```json
{
  "question": "Mit oder ohne Tests?",
  "header": "Tests",
  "multiSelect": false,
  "options": [
    {"label": "Mit Tests", "description": "TDD-Ansatz"},
    {"label": "Ohne Tests", "description": "Nur Implementierung"},
    {"label": "egal", "description": "AI entscheidet"}
  ]
}
```

**d) Stop-Check**: Sind noch relevante Unklarheiten? Wenn ja → zurueck zu a). Wenn nein → weiter zu Schritt 4.

### Regeln fuer Fragen

- **JEDE Frage hat IMMER eine "egal / AI entscheidet" Option** — der User soll nie gezwungen sein, eine Meinung zu haben
- Fragen sind kurz: maximal 15 Woerter
- 2-4 Optionen pro Frage
- Nie nach etwas fragen, das der Prompt bereits klaert
- Du entscheidest den Einstieg: Domaene, Intent-Check, oder direkt Ambiguitaeten — was am meisten Informationsgewinn bringt
- Maximal ~5-7 Runden. Du sollst vorher stoppen wenn genug Klarheit herrscht. Das ist ein Safety-Cap, kein Ziel.

### 4. Antworten

Bearbeite den urspruenglichen Prompt. Wende alle gesammelten Informationen an:

- **besonders wichtig**: Maximaler Aufwand, produktionsreife Qualitaet. Bekommt den meisten Raum.
- **relevant**: Sorgfaeltig und durchdacht umsetzen.
- **egal**: AI hat volle kreative Freiheit. Nutze dein bestes Urteil — das ist kein "unwichtig", sondern "du darfst entscheiden".
- **nicht relevant**: Investiere keinen Aufwand. Ueberspringe oder minimiere.
- **Inhaltliche Entscheidungen**: Folge der gewaehlten Richtung.

Erwaehne die Fragen und Bewertungen NICHT — lass sie unsichtbar dein Verhalten steuern.
