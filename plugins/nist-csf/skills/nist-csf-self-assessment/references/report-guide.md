# Filling the report template (no code execution required)

The report is produced by copying `references/report-template.html` and replacing every
`{{TOKEN}}` with a value, following the rules below. Do not restructure the HTML, change
the CSS, or redesign anything — fixed structure is what keeps reports comparable and
on-brand across agencies and across models. When done, verify the output contains no
remaining `{{` and save it as `report.html`.

## 1. Compute scores (simple averaging, one decimal place)

- **Question score** = the 1–4 tier the user confirmed. N/A and unanswered questions are excluded everywhere below.
- **Category score** = mean of its questions' scores, rounded to 1 decimal. (Categories with two questions: GV.SC = GV-6 & GV-7 · ID.AM = ID-1 & ID-2 · ID.RA = ID-3 & ID-4 · PR.AA = PR-1 & PR-2 · PR.DS = PR-4 & PR-5 · PR.PS = PR-6 & PR-7 · DE.CM = DE-1 & DE-2 · DE.AE = DE-3 & DE-4 · RS.MA = RS-1 & RS-2 · RC.RP = RC-1 & RC-2 · RC.CO = RC-3 & RC-4. Every other category equals its single question's score.)
- **Function score** = mean of its category scores, 1 decimal.
- **Overall score** = mean of the six function scores, 1 decimal.
- Show every score with one decimal (e.g. `3` → `3.0`). If a category/function has no answered questions, its score is `n/a`.

## 2. Tier labels and colors (floored, never rounded up)

Take the whole-number part of the score (2.9 → 2), then:

| Floor | Label token value | Color token value |
|---|---|---|
| 1 | Tier 1 – Partial | `#c0392b` |
| 2 | Tier 2 – Risk Informed | `#e67e22` |
| 3 | Tier 3 – Repeatable | `#b8a41c` |
| 4 | Tier 4 – Adaptive | `#2e7d46` |
| n/a | n/a | `#888888` |

## 3. Token reference

- `{{ORG}} {{SCOPE}} {{ASSESSOR}} {{DATE}}` — from intake. If assessor or scope wasn't given, delete that `<span>`.
- `{{OVERALL_SCORE}} {{OVERALL_COLOR}} {{OVERALL_LABEL}}` — overall score, its color, its label.
- Per function (GOVERN…RECOVER): `{{GOVERN_SCORE}}` `{{GOVERN_COLOR}}` `{{GOVERN_LABEL}}` and radar point `{{GOVERN_X}}` `{{GOVERN_Y}}` — X/Y come from the lookup tables in §5 (round the function score to 1 decimal first; n/a → 280, 280).
- Per category (token = code with `_`, e.g. `GV_OC`): `{{GV_OC_SCORE}}` `{{GV_OC_COLOR}}` `{{GV_OC_PCT}}` — PCT is the bar width from §4.
- Per question (token = ID without dash, e.g. `GV1`): `{{GV1_SCORE}}` (the 1–4 digit, `N/A`, or `—` if unanswered), `{{GV1_COLOR}}`, `{{GV1_NOTE}}` (the user's note verbatim, or delete the note `<div>` per the inline comment).
- Strengths / mitigations / help blocks / partial flag: follow the HTML comments in the template — they say exactly what to copy, fill, or delete. Mitigation text comes from each question's **If low** line in `references/questions.md`, condensed to 1–2 sentences; the six *(priority)* questions are ID-1, PR-1, PR-5, PR-7, DE-2, RS-1.

## 4. Bar width percentages (`*_PCT`, score → width)

1.0→25% · 1.1→28% · 1.2→30% · 1.3→32% · 1.4→35% · 1.5→38% · 1.6→40% · 1.7→42% · 1.8→45% · 1.9→48% · 2.0→50% · 2.1→52% · 2.2→55% · 2.3→57% · 2.4→60% · 2.5→62% · 2.6→65% · 2.7→68% · 2.8→70% · 2.9→72% · 3.0→75% · 3.1→78% · 3.2→80% · 3.3→82% · 3.4→85% · 3.5→88% · 3.6→90% · 3.7→92% · 3.8→95% · 3.9→98% · 4.0→100%

n/a → `0%`.

## 5. Radar point lookup tables (`*_X`, `*_Y`)

Round the function score to one decimal, find the row, copy x and y exactly. n/a → x 280, y 280.

**GOVERN axis** (score → x, y for the radar point)

| score | x | y |  | score | x | y |
|---|---|---|---|---|---|---|
| 1.0 | 280 | 230 |  | 2.6 | 280 | 149 |
| 1.1 | 280 | 224 |  | 2.7 | 280 | 144 |
| 1.2 | 280 | 219 |  | 2.8 | 280 | 139 |
| 1.3 | 280 | 214 |  | 2.9 | 280 | 134 |
| 1.4 | 280 | 209 |  | 3.0 | 280 | 128 |
| 1.5 | 280 | 204 |  | 3.1 | 280 | 123 |
| 1.6 | 280 | 199 |  | 3.2 | 280 | 118 |
| 1.7 | 280 | 194 |  | 3.3 | 280 | 113 |
| 1.8 | 280 | 189 |  | 3.4 | 280 | 108 |
| 1.9 | 280 | 184 |  | 3.5 | 280 | 103 |
| 2.0 | 280 | 179 |  | 3.6 | 280 | 98 |
| 2.1 | 280 | 174 |  | 3.7 | 280 | 93 |
| 2.2 | 280 | 169 |  | 3.8 | 280 | 88 |
| 2.3 | 280 | 164 |  | 3.9 | 280 | 83 |
| 2.4 | 280 | 159 |  | 4.0 | 280 | 78 |
| 2.5 | 280 | 154 |  |  | |  |

**IDENTIFY axis** (score → x, y for the radar point)

| score | x | y |  | score | x | y |
|---|---|---|---|---|---|---|
| 1.0 | 324 | 255 |  | 2.6 | 394 | 214 |
| 1.1 | 328 | 252 |  | 2.7 | 398 | 212 |
| 1.2 | 332 | 250 |  | 2.8 | 402 | 209 |
| 1.3 | 337 | 247 |  | 2.9 | 407 | 207 |
| 1.4 | 341 | 245 |  | 3.0 | 411 | 204 |
| 1.5 | 346 | 242 |  | 3.1 | 416 | 202 |
| 1.6 | 350 | 240 |  | 3.2 | 420 | 199 |
| 1.7 | 354 | 237 |  | 3.3 | 424 | 197 |
| 1.8 | 359 | 235 |  | 3.4 | 429 | 194 |
| 1.9 | 363 | 232 |  | 3.5 | 433 | 192 |
| 2.0 | 367 | 230 |  | 3.6 | 437 | 189 |
| 2.1 | 372 | 227 |  | 3.7 | 442 | 187 |
| 2.2 | 376 | 224 |  | 3.8 | 446 | 184 |
| 2.3 | 381 | 222 |  | 3.9 | 451 | 182 |
| 2.4 | 385 | 219 |  | 4.0 | 455 | 179 |
| 2.5 | 389 | 217 |  |  | |  |

**PROTECT axis** (score → x, y for the radar point)

| score | x | y |  | score | x | y |
|---|---|---|---|---|---|---|
| 1.0 | 324 | 305 |  | 2.6 | 394 | 346 |
| 1.1 | 328 | 308 |  | 2.7 | 398 | 348 |
| 1.2 | 332 | 310 |  | 2.8 | 402 | 351 |
| 1.3 | 337 | 313 |  | 2.9 | 407 | 353 |
| 1.4 | 341 | 315 |  | 3.0 | 411 | 356 |
| 1.5 | 346 | 318 |  | 3.1 | 416 | 358 |
| 1.6 | 350 | 320 |  | 3.2 | 420 | 361 |
| 1.7 | 354 | 323 |  | 3.3 | 424 | 363 |
| 1.8 | 359 | 325 |  | 3.4 | 429 | 366 |
| 1.9 | 363 | 328 |  | 3.5 | 433 | 368 |
| 2.0 | 367 | 330 |  | 3.6 | 437 | 371 |
| 2.1 | 372 | 333 |  | 3.7 | 442 | 373 |
| 2.2 | 376 | 336 |  | 3.8 | 446 | 376 |
| 2.3 | 381 | 338 |  | 3.9 | 451 | 378 |
| 2.4 | 385 | 341 |  | 4.0 | 455 | 381 |
| 2.5 | 389 | 343 |  |  | |  |

**DETECT axis** (score → x, y for the radar point)

| score | x | y |  | score | x | y |
|---|---|---|---|---|---|---|
| 1.0 | 280 | 330 |  | 2.6 | 280 | 411 |
| 1.1 | 280 | 336 |  | 2.7 | 280 | 416 |
| 1.2 | 280 | 341 |  | 2.8 | 280 | 421 |
| 1.3 | 280 | 346 |  | 2.9 | 280 | 426 |
| 1.4 | 280 | 351 |  | 3.0 | 280 | 432 |
| 1.5 | 280 | 356 |  | 3.1 | 280 | 437 |
| 1.6 | 280 | 361 |  | 3.2 | 280 | 442 |
| 1.7 | 280 | 366 |  | 3.3 | 280 | 447 |
| 1.8 | 280 | 371 |  | 3.4 | 280 | 452 |
| 1.9 | 280 | 376 |  | 3.5 | 280 | 457 |
| 2.0 | 280 | 381 |  | 3.6 | 280 | 462 |
| 2.1 | 280 | 386 |  | 3.7 | 280 | 467 |
| 2.2 | 280 | 391 |  | 3.8 | 280 | 472 |
| 2.3 | 280 | 396 |  | 3.9 | 280 | 477 |
| 2.4 | 280 | 401 |  | 4.0 | 280 | 482 |
| 2.5 | 280 | 406 |  |  | |  |

**RESPOND axis** (score → x, y for the radar point)

| score | x | y |  | score | x | y |
|---|---|---|---|---|---|---|
| 1.0 | 236 | 305 |  | 2.6 | 166 | 346 |
| 1.1 | 232 | 308 |  | 2.7 | 162 | 348 |
| 1.2 | 228 | 310 |  | 2.8 | 158 | 351 |
| 1.3 | 223 | 313 |  | 2.9 | 153 | 353 |
| 1.4 | 219 | 315 |  | 3.0 | 149 | 356 |
| 1.5 | 214 | 318 |  | 3.1 | 144 | 358 |
| 1.6 | 210 | 320 |  | 3.2 | 140 | 361 |
| 1.7 | 206 | 323 |  | 3.3 | 136 | 363 |
| 1.8 | 201 | 325 |  | 3.4 | 131 | 366 |
| 1.9 | 197 | 328 |  | 3.5 | 127 | 368 |
| 2.0 | 193 | 330 |  | 3.6 | 123 | 371 |
| 2.1 | 188 | 333 |  | 3.7 | 118 | 373 |
| 2.2 | 184 | 336 |  | 3.8 | 114 | 376 |
| 2.3 | 179 | 338 |  | 3.9 | 109 | 378 |
| 2.4 | 175 | 341 |  | 4.0 | 105 | 381 |
| 2.5 | 171 | 343 |  |  | |  |

**RECOVER axis** (score → x, y for the radar point)

| score | x | y |  | score | x | y |
|---|---|---|---|---|---|---|
| 1.0 | 236 | 255 |  | 2.6 | 166 | 214 |
| 1.1 | 232 | 252 |  | 2.7 | 162 | 212 |
| 1.2 | 228 | 250 |  | 2.8 | 158 | 209 |
| 1.3 | 223 | 247 |  | 2.9 | 153 | 207 |
| 1.4 | 219 | 245 |  | 3.0 | 149 | 204 |
| 1.5 | 214 | 242 |  | 3.1 | 144 | 202 |
| 1.6 | 210 | 240 |  | 3.2 | 140 | 199 |
| 1.7 | 206 | 237 |  | 3.3 | 136 | 197 |
| 1.8 | 201 | 235 |  | 3.4 | 131 | 194 |
| 1.9 | 197 | 232 |  | 3.5 | 127 | 192 |
| 2.0 | 193 | 230 |  | 3.6 | 123 | 189 |
| 2.1 | 188 | 227 |  | 3.7 | 118 | 187 |
| 2.2 | 184 | 224 |  | 3.8 | 114 | 184 |
| 2.3 | 179 | 222 |  | 3.9 | 109 | 182 |
| 2.4 | 175 | 219 |  | 4.0 | 105 | 179 |
| 2.5 | 171 | 217 |  |  | |  |

## 6. The markdown companion (`report.md`)

Also write a short plain-text summary:

```
# Cybersecurity Self-Assessment Report — <org>
<scope> · <date>

**Overall: <score> / 4.0 — <tier label>**

## Function scores
- GOVERN: <score> (<label>)
… (all six)

## Top mitigations
- **<title>** (<ID>, Tier <score>): <mitigation>
… (Act-now items first, then Plan-next)

---
This self-assessment is a point-in-time snapshot based on self-reported answers; it is
not an audit and does not certify compliance with any standard.
```

## 7. Final checks

1. Search the finished HTML for `{{` — zero occurrences allowed.
2. Every deleted-block instruction (partial flag, notes, empty subsections, non-matching help blocks) actually deleted, comments included.
3. Radar polygon has exactly six coordinate pairs and six circles matching them.
