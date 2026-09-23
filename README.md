# wacirt-nist-csf

Interactive **NIST CSF 2.0 self-assessment** for Claude — built for IT and
security staff at state and local government agencies, usable by any org.

33 questions condensed from all 22 CSF 2.0 categories · CSF Tier 1–4 scoring ·
plain-language help, examples, and example controls on every question ·
HTML report with radar chart, section scores, prioritized mitigations, and
where to get help (WaTech OCS, WA CIRT, MS-ISAC, CISA).

Maintained by a volunteer with the Washington Cybersecurity Incident Response
Team (WA CIRT); not an official product of any agency.

## Install — Claude Desktop / Cowork (paid Claude plans)

The desktop app manages plugins through its UI, not slash commands:

1. Open **Customize** in the sidebar, then **Plugins** (also reachable from
   the **+** button next to the prompt box in a Cowork conversation).
2. Choose **Add marketplace** and enter:
   `https://github.com/pikepinesw/wacirt-nist-csf`
3. Find **nist-csf** in the marketplace listing and install it; confirm it
   shows as enabled (Manage plugins to enable/disable/uninstall later).
4. Start a new Cowork session and say **"run a NIST CSF self-assessment"**
   (natural language is the reliable trigger; slash invocation of plugin
   skills in Cowork can be flaky).

Reports are saved to a `wacirt-nist-csf-reports` folder in your home
directory (in sandboxed sessions, Claude will tell you where they landed).

## Install — Claude Code (terminal)

    /plugin marketplace add pikepinesw/wacirt-nist-csf
    /plugin install nist-csf@wacirt-nist-csf

Restart the session, then run `/nist-csf:assess` — or just ask for
"a NIST CSF self-assessment."

Note: Claude Code and Desktop/Cowork installs are independent — installing
in one does not install it in the other.

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

Claude Desktop / Cowork: **Customize → Plugins → Manage plugins** →
uninstall, then remove the marketplace.

Claude Code:

    /plugin uninstall nist-csf@wacirt-nist-csf
    /plugin marketplace remove wacirt-nist-csf

## References

**Claude plugin & skill documentation**

- Plugins: https://docs.claude.com/en/docs/claude-code/plugins
- Plugin marketplaces (manifest schema): https://docs.claude.com/en/docs/claude-code/plugin-marketplaces
- Agent Skills in Claude Code: https://docs.claude.com/en/docs/claude-code/skills
- Slash commands: https://docs.claude.com/en/docs/claude-code/slash-commands
- Claude help center (Cowork, plans, features): https://support.claude.com

**Framework & security resources used by this assessment**

- NIST Cybersecurity Framework 2.0: https://www.nist.gov/cyberframework
- WA CIRT / WA Military Department cybersecurity program: https://mil.wa.gov/cyber-security-program
- WaTech Office of Cybersecurity (WA state agencies): https://watech.wa.gov
- MS-ISAC (free for SLTT governments): https://www.cisecurity.org/ms-isac
- CISA Cyber Hygiene services (free): https://www.cisa.gov/cyber-hygiene-services
- CISA Known Exploited Vulnerabilities catalog: https://www.cisa.gov/known-exploited-vulnerabilities-catalog
- CIS Controls: https://www.cisecurity.org/controls

## License

Apache License 2.0 — see LICENSE.