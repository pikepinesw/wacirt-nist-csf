---
name: nist-csf-self-assessment
description: Run an interactive NIST Cybersecurity Framework (CSF) 2.0 self-assessment and produce a scored HTML report with a radar chart, section scores, prioritized mitigations, and where to get help. Use this skill whenever the user asks for a security self-assessment, security posture or maturity review, NIST CSF check, cyber health check, security scorecard, gap assessment, or a radar/spider chart of their security program — even if they never say "NIST." Designed for IT and security staff at state and local government agencies, but works for any organization.
---

# NIST CSF 2.0 Self-Assessment

Guide the user through a condensed (~33 question) NIST CSF 2.0 self-assessment covering all six functions — Govern, Identify, Protect, Detect, Respond, Recover — scored on CSF Tiers 1–4, then generate a report with a radar chart, category scores, prioritized mitigations, and how to get help.

The audience is IT and security staff, often at state agencies. Some are seasoned CISOs; some are a one-person IT shop wearing the security hat. Never assume expertise, never condescend. Every question comes with plain-language help they can ask for.

## Where files are saved

All files this skill produces (the state file and both reports) are saved to a folder named `wacirt-nist-csf-reports` in the user's home directory — `/Users/<name>/wacirt-nist-csf-reports` on macOS, `C:\Users\<name>\wacirt-nist-csf-reports` on Windows, `~/wacirt-nist-csf-reports` on Linux. Create the folder if it doesn't exist. If the environment is sandboxed and cannot reach the home directory (e.g., a Cowork session), save to the session's normal output location instead and tell the user exactly where the files are.

## What this produces

1. A completed answer file (`assessment-state.json`) — the raw record, kept in the reports folder so an interrupted assessment can be resumed.
2. `report-DATE.html` — polished, print-friendly report: radar chart of the six functions, category-level scores, strengths, gaps, prioritized mitigations, and a "getting help" section.
3. `report-DATE.md` — plain-text summary of the same, for email or ticket systems.

`DATE` is today's date as `YYYY-MM-DD`, so each run writes unique files and scores can be compared over time. If a report for today already exists, append `-2`, `-3`, … rather than overwriting.

## Step 1 — Intake

Before the first question, collect (briefly, don't interrogate):

- **Organization / agency name**
- **Scope** — whole agency, one division, one system? (Write it down; scope creep ruins assessments.)
- **Assessor name(s)** and role (optional)
- **Sector** — Washington state agency, other state agency, local government / special district, K-12 / higher-ed, tribal, other. This tailors the "getting help" section of the report.

Then, before explaining the scale, tell the user in one line that help is always available — for example: *"At any point during the assessment, just say 'explain more', 'give me examples', or 'what controls count' and I'll help before you answer."*

Then explain the scale once, in one short block:

> **Scoring: CSF Tiers 1–4.** For each question, answer with a tier or just describe what you do and I'll suggest a tier.
> **1 – Partial:** ad hoc, reactive, depends on individuals.
> **2 – Risk Informed:** practices exist and are approved, but not consistent agency-wide.
> **3 – Repeatable:** formal policy, done consistently, reviewed and updated.
> **4 – Adaptive:** continuously improved, measured, informed by lessons learned and threat intel.
> At any question you can say **explain** (what it means and why it matters), **examples** (what each tier looks like), **controls** (example controls that satisfy it), **skip** or **n/a**.

## Step 2 — Run the interview

The full question bank is in `references/questions.md`. Read the section for the current function before asking its questions — each entry has the question text, a plain-language explanation, tier anchors, example controls, and "if scored low" guidance. Ask the questions as written (light rephrasing to fit conversation is fine; don't change their meaning — scores must stay comparable across agencies).

Interview mechanics:

- **One question at a time** by default. Announce each function as you enter it ("Function 2 of 6: IDENTIFY — 5 questions"). If the user asks to go faster, you may batch a category's questions together, but never a whole function.
- **Accept prose answers.** If the user describes their practice instead of giving a number, propose a tier with one sentence of reasoning, and anchor the suggestion by briefly stating what Tier 1 (LOW) and Tier 4 (HIGH) look like for that specific question — drawn from its Tier anchors in `references/questions.md` — then ask them to confirm or adjust. The user always owns the final score — this is a *self*-assessment.
- **Helper requests** — accept the keywords and natural variants of them: `explain` / "explain more" / "why does this matter", `examples` / "give me examples" / "what does each tier look like", `controls` / "what controls count". Answer from the question's entry in `references/questions.md`, in your own words, sized to what they asked. Then re-ask the question. If they ask something beyond the reference (e.g., "does Intune count?"), answer from general knowledge — that's exactly the value of running this interactively.
- **Half-tiers are not allowed.** If they're torn between two tiers, the lower one is the honest answer; note the reason in `notes`.
- **Capture notes.** When the user volunteers detail ("we have MFA except for the AS/400"), record a one-line note with the answer — notes make the report dramatically more useful.
- **N/A** is allowed but rare; ask why and record the reason. N/A questions are excluded from averages.
- Keep your own tone brisk and neutral. Low scores are normal and expected — say so if the user seems discouraged. A first assessment averaging Tier 2 is typical.

### Saving state

After intake and after **each function** (not each question), write/update `assessment-state.json` in the `wacirt-nist-csf-reports` folder (see "Where files are saved") so a crash or interruption loses at most one function:

```json
{
  "org": "Department of Examples",
  "scope": "Agency-wide",
  "assessor": "J. Smith, IT Manager",
  "sector": "wa-state-agency",
  "date": "2026-09-20",
  "answers": [
    {"id": "GV-1", "score": 2, "notes": "Mission documented; reg mapping incomplete"},
    {"id": "GV-2", "score": null, "na_reason": "…", "notes": ""}
  ]
}
```

`sector` is one of: `wa-state-agency`, `state-agency`, `local-gov`, `education`, `tribal`, `other`. Use `score: null` only for N/A.

If an `assessment-state.json` already exists in that folder when the skill starts, offer to resume from where it left off.

## Step 3 — Generate the report

When all questions are answered (or the user stops early — a partial report is allowed, flag it as partial), produce the report by **filling in the template — no code execution and no dependencies required**:

1. Read `references/report-guide.md` in full. It contains the scoring math, the tier label/color mapping, the token reference, and precomputed lookup tables for the radar chart coordinates and bar widths — everything is table lookups and simple averaging, no trigonometry, no scripts.
2. Copy `references/report-template.html` and replace every `{{TOKEN}}`, following the guide and the HTML comments embedded in the template (they say what to fill, copy, or delete). Do not restructure the HTML or restyle it — the fixed design is deliberate.
3. Save as `report-DATE.html`, and write the short `report-DATE.md` companion per the guide — both into the `wacirt-nist-csf-reports` folder (see "Where files are saved"), where `DATE` is today's date as `YYYY-MM-DD`.
4. Run the guide's final checks — above all, the finished HTML must contain no remaining `{{`.

Scoring (also in the guide): category score = mean of its questions; function score = mean of its category scores (so a category with two questions doesn't outweigh one with one); overall = mean of function scores. One decimal everywhere; tier labels are floored, never rounded up.

Then:
1. Sanity-check the output (spot-check the radar polygon and one mitigation).
2. Deliver both files to the user, naming the folder and filenames explicitly.
3. In chat, give a 3–5 sentence executive summary: overall tier, strongest and weakest function, and the top 2–3 "act now" items. Do not recite the whole report.

## Step 4 — Discuss mitigations

The report lists mitigations for everything scored ≤ 2, split into **Act now** (high-priority basics: MFA, backups, patching, monitoring, IR plan, inventory) and **Plan next**. After delivering, offer to go deeper on any item — sequencing, cheap/free options (CIS Controls IG1, MS-ISAC membership is free for SLTT governments), or drafting a remediation plan. This conversation is often more valuable than the report; don't skip the offer.

## Customization (for the skill owner)

- The "Getting help" contact blocks and footer live directly in `references/report-template.html` — edit the HTML there (each block's comment says which sectors it applies to). Branding, colors, and layout are all in the same file's CSS.
- Questions live in `references/questions.md`; the six *(priority)* markers there drive the "Act now" mitigation grouping. If you renumber or restructure questions, also update the category-membership list in `references/report-guide.md` §1 and the fixed rows in the template.

## Portability

This skill is deliberately dependency-free: the interview logic lives in this file and `references/questions.md`, and the report is produced by filling `references/report-template.html` using the lookup tables in `references/report-guide.md` — no Python, no installs, no network, no code execution of any kind. Any model/harness that can read markdown and write a text file can run the whole thing, including on locked-down state-agency machines and air-gapped environments. To ship it elsewhere, copy the folder.