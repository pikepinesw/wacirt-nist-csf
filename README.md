# csf-plugins

Claude plugin marketplace: security assessment skills for state & local government IT/security teams.

## Install (Claude Code or Cowork)

    /plugin marketplace add HEATH-GITHUB-USERNAME/csf-plugins
    /plugin install nist-csf@csf-plugins

Then run `/nist-csf:assess` (or just ask for "a NIST CSF self-assessment").

## Standalone / local models

The skill in `plugins/nist-csf/skills/nist-csf-self-assessment/` is self-contained:
plain-markdown instructions plus an HTML report template the model fills in directly.
No Python, no packages, no network, no code execution — any agent harness that can
read markdown and write a text file can run it, including air-gapped.
