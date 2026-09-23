---
description: Run the NIST CSF 2.0 cybersecurity self-assessment and produce a scored report
---
Use the nist-csf-self-assessment skill to run a full interactive NIST CSF 2.0 self-assessment, exactly as the skill's SKILL.md describes: intake, one question at a time with explain/examples/controls helpers, CSF Tier 1-4 scoring, then generate the HTML + markdown report.

If the user supplied arguments ($ARGUMENTS), treat them as intake context (organization name, scope, or sector) and confirm before starting the questions. If an assessment-state.json exists in the working directory, offer to resume it.
