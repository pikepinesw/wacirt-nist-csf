# wacirt-nist-csf

Interactive **NIST CSF 2.0 self-assessment** for Claude — built for IT and
security staff at state and local government agencies, usable by any org.

33 questions condensed from all 22 CSF 2.0 categories · CSF Tier 1–4 scoring ·
plain-language help, examples, and example controls on every question ·
HTML report with radar chart, section scores, prioritized mitigations, and
where to get help (WaTech OCS, WA CIRT, MS-ISAC, CISA).

Maintained by a volunteer with the Washington Cybersecurity Incident Response
Team (WA CIRT); not an official product of any agency.

## Install (Claude Code or Claude Cowork — paid Claude plans)

    /plugin marketplace add pikepinesw/wacirt-nist-csf
    /plugin install nist-csf@wacirt-nist-csf

Restart the session, then run `/nist-csf:assess` — or just ask for
"a NIST CSF self-assessment." Reports are saved to a
`wacirt-nist-csf-reports` folder in your home directory.

## Free / local-model use (no Claude subscription)

The skill is deliberately dependency-free: plain-markdown instructions plus an
HTML report template the model fills in directly. No Python, no packages, no
network, no code execution — any agent harness that can read markdown and
write a text file can run it, including air-gapped.

Point your harness at:

    plugins/nist-csf/skills/nist-csf-self-assessment/SKILL.md

## Repo layout

    .claude-plugin/marketplace.json      — marketplace manifest
    plugins/nist-csf/
      .claude-plugin/plugin.json         — plugin manifest
      commands/assess.md                 — /nist-csf:assess command
      skills/nist-csf-self-assessment/
        SKILL.md                         — interview + workflow
        references/questions.md          — question bank (anchors, controls, mitigations)
        references/report-template.html  — fill-in-the-blanks report (edit branding/contacts here)
        references/report-guide.md       — scoring rules + radar lookup tables

## Customizing for your org

Edit the "Getting help" blocks and CSS in `references/report-template.html`,
and the questions in `references/questions.md` (keep `report-guide.md` §1 and
the template's fixed rows in sync if you restructure).

## Uninstall

    /plugin uninstall nist-csf@wacirt-nist-csf
    /plugin marketplace remove wacirt-nist-csf

## License

Apache2.0 — see LICENSE.