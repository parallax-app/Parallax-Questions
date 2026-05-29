# Parallax Questions

Source-of-truth question bank for the Parallax relationship/personality assessment app. Each question is stored once per supported language and shares a stable `id` across languages so an answer in any locale maps to the same underlying prompt.

## Layout

```
questions-<lang>/
  1-Everyday life & habits.json       (80)
  2-Inner emotional world.json        (100)
  3-Past & Personal History.json      (80)
  4-Values & Beliefs.json             (100)
  5-Future & Goals.json               (100)
  6-Romance & Intimacy.json           (80)
  7-Personality.json                  (79)
  8-Relationship dynamics.json        (140)
  9-Social world.json                 (40)
  10-Body & wellbeing.json            (60)
  11-Shared history.json              (60)
  12-Tastes & Favorites.json          (80)
  13-Fun hypotheticals.json           (60)
```

**1,059 questions per language**, organized across 13 thematic files.

## Languages

| Code | Language          | Status     |
|------|-------------------|------------|
| en   | English           | source     |
| de   | German            | translated |
| es   | Spanish (LatAm)   | translated |
| fa   | Farsi (Persian)   | translated |
| hi   | Hindi             | translated |
| tr   | Turkish           | translated |
| zh   | Mandarin (Simpl.) | translated |
| ar   | Arabic            | pending    |
| fr   | French            | pending    |
| ja   | Japanese          | pending    |
| ru   | Russian           | pending    |

Translations target natural, conversational register for a native speaker — not literal word-for-word — and preserve each question's emotional tone (intimate / reflective / playful / vulnerable).

## Question schema

Each file is a JSON array of question objects:

```json
{
  "id": "spending_saving-001",
  "category": "finances",
  "text": "I get more satisfaction from saving money than from spending it.",
  "answer_type": "likert",
  "scale_low_label": "strongly disagree",
  "scale_high_label": "strongly agree",
  "options": null,
  "depth": "light",
  "weight": "reflective",
  "spice": 0,
  "language": "en",
  "tags": ["habits", "values", "money"],
  "status": "draft",
  "created_at": "2026-05-24T00:00:00Z",
  "updated_at": "2026-05-24T00:00:00Z",
  "contributor": "ai-generated"
}
```

### Fields

| Field             | Notes                                                                 |
|-------------------|-----------------------------------------------------------------------|
| `id`              | Stable identifier — same across all language files                    |
| `category`        | Top-level grouping (finances, family, etc.)                           |
| `text`            | The question prompt (translated per language)                         |
| `answer_type`     | `likert` \| `multiple_choice` \| `binary` \| `free_text`              |
| `scale_low_label` / `scale_high_label` | Anchor labels for likert; null otherwise          |
| `options`         | Array of choices for multiple_choice/binary; null otherwise           |
| `depth`           | `icebreaker` \| `light` \| `deep` \| `vulnerable`                     |
| `weight`          | `playful` \| `reflective` \| `revealing`                              |
| `spice`           | 0–3 — how intimate/sensitive the prompt is                            |
| `language`        | ISO code matching the parent folder                                   |
| `tags`            | Free-form labels for filtering and grouping                           |
| `status`          | Lifecycle marker (`draft`, etc.)                                      |
| `contributor`     | Author or generator source                                            |

## Translation invariants

When adding a new language:

- `id`, `category`, `answer_type`, `depth`, `weight`, `spice`, `tags`, `status`, `created_at`, `updated_at`, `contributor` are **identical** to the English source.
- `language` is set to the target ISO code.
- `text`, `scale_low_label`, `scale_high_label`, and every string in `options` are translated.
- `options` arrays match the English source **in count and order** (so option indexes are stable across locales).
- Null fields stay null.
