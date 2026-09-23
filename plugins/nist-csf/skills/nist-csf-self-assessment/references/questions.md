# NIST CSF 2.0 Condensed Question Bank (33 questions)

Contents: [GOVERN](#govern--7-questions) · [IDENTIFY](#identify--5-questions) · [PROTECT](#protect--8-questions) · [DETECT](#detect--4-questions) · [RESPOND](#respond--5-questions) · [RECOVER](#recover--4-questions)

Each entry: **Ask** (the question, as posed), **Explain** (plain-language meaning + why it matters, for the `explain` helper), **Tiers** (anchors for the `examples` helper), **Controls** (for the `controls` helper), **If low** (mitigation seed — the report carries a short version automatically).

Tier shorthand used below — T1 Partial · T2 Risk Informed · T3 Repeatable · T4 Adaptive.

---

## GOVERN — 7 questions

### GV-1 · GV.OC — Organizational context
**Ask:** Has your agency documented its mission-critical services and the legal, regulatory, and contractual cybersecurity obligations that apply to them?
**Explain:** You can't protect what you haven't defined. This is the list of "what must not fail" (payroll, 911 dispatch, benefits eligibility, permitting) plus the rules you're bound by — for WA agencies that includes WaTech SEC policies (OCIO 141.10 lineage), plus data-specific regimes like HIPAA, CJIS, IRS Pub 1075, FERPA, and PCI where applicable.
**Tiers:** T1: tribal knowledge, nothing written. T2: a partial list exists in someone's doc. T3: documented critical services + obligation mapping, reviewed on a schedule. T4: mapping drives investment decisions and is updated when law/mission changes.
**Controls:** Business impact analysis (BIA); data/system inventory tagged with applicable regulations; annual review tied to legislative session.
**If low:** Run a half-day workshop: list top 10 critical services, owner, and applicable regulations. One spreadsheet beats nothing.

### GV-2 · GV.RM — Risk management strategy
**Ask:** Does your agency have an approved cybersecurity risk management strategy — including a stated risk appetite and a maintained risk register?
**Explain:** This is how the agency decides which risks to fix, accept, transfer, or avoid — and who gets to accept them. Without it, risk acceptance happens silently by whoever is busiest.
**Tiers:** T1: risks handled ad hoc as they surface. T2: a risk register exists but isn't current or leadership-reviewed. T3: approved strategy, defined acceptance authority, register reviewed on a cadence. T4: risk data (metrics, incidents, threat intel) continuously reshapes priorities and budget.
**Controls:** Risk register with owner/likelihood/impact/treatment; documented risk-acceptance form signed above the IT level; annual risk assessment (WaTech's RiskManagement@watech.wa.gov offers this to WA agencies).
**If low:** Start a 10-line risk register and get one executive to formally own risk acceptance. Formalize the strategy after it's in use.

### GV-3 · GV.RR — Roles, responsibilities, and authorities
**Ask:** Are cybersecurity roles, responsibilities, and authorities defined, assigned to named people, and resourced — including a designated security lead?
**Explain:** Someone must own security with actual authority, and everyone else must know their part (managers approving access, HR in offboarding, staff reporting phish). "IT handles it" is not an answer during an incident at 2 a.m.
**Tiers:** T1: security is a side duty with no defined authority. T2: a lead is named but authority/backfill are fuzzy. T3: documented RACI or equivalent, security lead with charter and budget line. T4: responsibilities extend into every business unit and are part of performance expectations.
**Controls:** Appointed ISO/security manager in writing; RACI for security processes; security responsibilities in job descriptions; deputy/backup named.
**If low:** Get a one-page memo from the agency head naming the security lead and their authority. It costs nothing and changes everything downstream.

### GV-4 · GV.PO — Policy
**Ask:** Is there an approved, current cybersecurity policy set that is communicated to staff and actually enforced?
**Explain:** Policy turns good intentions into requirements — acceptable use, access control, data handling, incident reporting. "Enforced" is the key word: a policy nobody follows scores like a policy that doesn't exist.
**Tiers:** T1: no policy, or a decade-old binder. T2: policies exist but staff don't know them; exceptions unmanaged. T3: approved, reviewed on a cycle, acknowledged by staff, exceptions tracked. T4: policy compliance measured; policies updated from incidents and audits.
**Controls:** Policy suite mapped to a framework (WA agencies: WaTech SEC policy series); annual staff acknowledgment; documented exception process with expiry dates.
**If low:** Don't write 20 policies. Adopt/adapt a template set (state policy, SANS, CIS) for the top 5: acceptable use, access, data handling, incident reporting, remote work.

### GV-5 · GV.OV — Oversight
**Ask:** Does agency leadership regularly review cybersecurity performance — metrics, audit findings, incident trends — and adjust direction based on them?
**Explain:** Governance means leaders look at security results and steer, not just fund it and hope. This is what separates a program from a pile of tools.
**Tiers:** T1: leadership hears about security only during incidents. T2: occasional briefings, no standing agenda. T3: recurring leadership review with defined metrics and follow-up on findings. T4: outcomes drive strategy/budget; independent audit results tracked to closure.
**Controls:** Quarterly security scorecard to executives; audit finding tracker with due dates; security standing item in leadership meetings.
**If low:** Book a recurring 30-minute quarterly briefing with 5 metrics (patching, MFA coverage, phish rate, open findings, incidents). Consistency matters more than sophistication.

### GV-6 · GV.SC — Supply chain risk program
**Ask:** Do you identify and risk-assess your technology suppliers and service providers before and during use?
**Explain:** Your security now includes your vendors' security — SaaS, MSPs, payment processors, that one SolarWinds-shaped dependency. You need to know who they are and which ones can hurt you most.
**Tiers:** T1: no vendor list; procurement doesn't ask security questions. T2: informal review of big vendors only. T3: vendor inventory, tiered by criticality/data access, assessed on a defined process. T4: continuous monitoring of critical vendors; concentration risk considered.
**Controls:** Vendor inventory with data-access tiering; security questionnaire or SOC 2/StateRAMP review in procurement; WA agencies: security design review (sdr@watech.wa.gov) for new systems.
**If low:** List every vendor that touches agency data, mark the five most critical, and review those five first.

### GV-7 · GV.SC — Supplier contract requirements
**Ask:** Do contracts with suppliers include cybersecurity requirements — including breach notification timelines — and do you verify them?
**Explain:** If it's not in the contract, you can't demand it during an incident. Notification timelines, data handling, return/destruction of data, and audit rights are the minimum.
**Tiers:** T1: standard vendor paper, no security terms. T2: security terms in some new contracts, legacy untouched. T3: standard security/data terms in all applicable contracts, notification SLAs defined. T4: terms verified (attestation/audit) and exercised; flow-down to subcontractors.
**Controls:** Standard data security contract addendum; 24–72h breach notification clause; DES/state master contract security terms where available.
**If low:** Work with contracts staff to adopt a standard security addendum for all new/renewing agreements — renewals are your leverage point.

---

## IDENTIFY — 5 questions

### ID-1 · ID.AM — Hardware & software inventory  *(priority)*
**Ask:** Do you maintain a current inventory of hardware, software, and cloud services — and would you notice an unauthorized one?
**Explain:** The unmanaged laptop and the forgotten server are where incidents start, and unknown assets never get patched. This is CIS Control #1 for a reason.
**Tiers:** T1: no reliable inventory. T2: spreadsheet, updated when someone remembers. T3: tool-based inventory (MDM/RMM/vuln scanner) reconciled on a schedule; unauthorized assets flagged. T4: near-real-time discovery; deviations alert automatically.
**Controls:** MDM/endpoint agent coverage; network discovery scans; cloud asset inventory (native tools); software allowlisting on high-risk systems.
**If low:** Deploy discovery before perfection: your vuln scanner, MDM, or even nmap can build the first inventory in a week.

### ID-2 · ID.AM — Data inventory & classification
**Ask:** Do you know what sensitive data you hold, where it lives, how it's classified, and how it flows — including to third parties?
**Explain:** Breach notification law (in WA: RCW 19.255 / 42.56.590) cares about *data*, not servers. You can't answer "what was on that box?" during an incident if you never mapped it. WA agencies have a required data classification scheme (Categories 1–4).
**Tiers:** T1: unknown; data lives wherever it landed. T2: major systems known; shares/exports unmapped. T3: classified inventory of sensitive data stores and flows, reviewed periodically. T4: discovery tooling finds sensitive data drift; classification drives handling automatically.
**Controls:** Data inventory tied to system inventory; WA data classification standard (Cat 1–4); data flow diagrams for top systems; DLP or data discovery scans.
**If low:** Inventory the top 5 systems holding Category 3/4 (confidential) data first — that's where breach risk and notification duty concentrate.

### ID-3 · ID.RA — Vulnerability & threat identification
**Ask:** Do you continuously identify vulnerabilities (scanning) and receive threat intelligence relevant to your environment?
**Explain:** You need two feeds: what's weak inside (vuln scans) and what's being attacked outside (threat intel). For SLTT governments, MS-ISAC membership is free and includes advisories and services.
**Tiers:** T1: no scanning; vulnerabilities found by attackers. T2: occasional or partial scans; no intel feed. T3: authenticated scanning on a schedule across the estate; subscribed to MS-ISAC/CISA advisories and acting on them. T4: continuous scanning incl. external attack surface; intel drives hunting and prioritization.
**Controls:** Authenticated vuln scanning (internal + external); MS-ISAC membership; CISA Known Exploited Vulnerabilities (KEV) tracking; CISA Cyber Hygiene (free external scanning).
**If low:** Sign up for MS-ISAC and CISA Cyber Hygiene this week — both free — and stand up a scanner against your server estate.

### ID-4 · ID.RA — Risk assessment & response
**Ask:** Are identified risks and vulnerabilities assessed, prioritized, and given a documented response (fix, accept, mitigate) with an owner?
**Explain:** Finding problems is easy; the program lives or dies on what happens next. A 400-page scan report with no owners is Tier 1 with extra steps.
**Tiers:** T1: findings pile up untriaged. T2: severe items fixed ad hoc; no documented decisions. T3: defined prioritization (severity × exposure, KEV first), remediation SLAs, documented acceptance for the rest. T4: risk-based prioritization using exploitability/business context; trends measured.
**Controls:** Remediation SLAs by severity; KEV-first policy; risk acceptance sign-off; monthly vulnerability metrics.
**If low:** Adopt one rule today: anything on CISA's KEV list gets fixed in 14 days or gets a signed risk acceptance.

### ID-5 · ID.IM — Improvement
**Ask:** Do lessons from incidents, exercises, audits, and assessments actually turn into tracked improvements?
**Explain:** CSF 2.0 moved "lessons learned" here to make the point: improvement is a discipline, not a meeting. If the last tabletop's action items are unfindable, that's your answer.
**Tiers:** T1: same issues recur; no after-action process. T2: after-action discussions happen, actions evaporate. T3: after-action reports with owners/dates, tracked to closure; this assessment repeated on a cadence. T4: improvement backlog prioritized alongside project work; effectiveness measured.
**Controls:** After-action report template; improvement/POA&M tracker; annual reassessment (this skill!) with score-over-score comparison.
**If low:** Create a single improvement tracker and put this assessment's mitigation list in it as entry one.

---

## PROTECT — 8 questions

### PR-1 · PR.AA — Identity, credentials & MFA  *(priority)*
**Ask:** Are identities and credentials centrally managed, and is phishing-resistant or app-based MFA enforced — especially for email, remote access, and admin accounts?
**Explain:** Stolen credentials are the #1 way in. MFA on email, VPN, and admin accounts blocks the large majority of account-takeover attacks. "Enforced" means required, not available.
**Tiers:** T1: passwords only, shared accounts exist. T2: MFA on some systems or optional. T3: MFA enforced for email/remote/admin, central IdP, joiner-mover-leaver process. T4: phishing-resistant MFA (FIDO2), conditional access, dormant accounts auto-disabled.
**Controls:** Central IdP (Entra ID/Okta); MFA enforcement policies; disable legacy auth; automated offboarding tied to HR.
**If low:** Enforce MFA on email and remote access first — this is the single highest-value control on this list. Then admin accounts, then everything else.

### PR-2 · PR.AA — Least privilege & privileged access
**Ask:** Is access granted on least privilege, reviewed periodically, and is administrative access separated and tightly controlled?
**Explain:** Everyone-is-admin means every phish is a domain compromise. Admin accounts should be separate from daily-driver accounts, few in number, and audited.
**Tiers:** T1: broad access, local admin common, no reviews. T2: some role-based access; admin sprawl unmeasured. T3: RBAC, separate admin accounts, no routine local admin, periodic access reviews with revocations. T4: just-in-time/PAM for privileged access, reviews automated, anomalous use alerts.
**Controls:** Separate -adm accounts; remove standing local admin (LAPS for local passwords); quarterly access recertification for sensitive systems; PAM tooling.
**If low:** Count your domain/global admins this week; get the number under 5 dedicated accounts and remove standing local admin from user endpoints.

### PR-3 · PR.AT — Awareness & training
**Ask:** Do all staff get security awareness training (including phishing), with extra role-based training for admins, developers, and finance?
**Explain:** Staff are your sensor network and your attack surface at once. Finance staff wiring money and admins holding keys need more than the annual generic module.
**Tiers:** T1: none, or once at hire. T2: annual module, no reinforcement, no role-based content. T3: annual training + phishing simulations + role-based content; completion tracked. T4: training adapted to observed behavior and current threats; reporting culture measured and healthy.
**Controls:** Annual training with tracked completion; phishing simulation program; targeted training for wire-transfer/payroll staff (BEC) and IT admins.
**If low:** Start with the two highest-loss scenarios: BEC training for anyone who moves money, and a "report phish" button for everyone.

### PR-4 · PR.DS — Data protection & encryption
**Ask:** Is sensitive data encrypted at rest and in transit, with managed keys, and are protections applied per its classification?
**Explain:** Encryption is the difference between "lost laptop" and "reportable breach." At rest: disks, databases, backups. In transit: TLS everywhere, no legacy protocols carrying credentials.
**Tiers:** T1: unencrypted laptops/shares/backups. T2: some encryption, coverage unknown. T3: full-disk encryption enforced on endpoints, TLS enforced, sensitive DBs/backups encrypted, key management defined. T4: encryption verified by monitoring; data handling automated from classification.
**Controls:** BitLocker/FileVault enforced via MDM; TLS 1.2+ minimum; encrypted backups; WA agencies: WaTech encryption standard (SEC-08-02-S).
**If low:** Enforce full-disk encryption on every laptop via MDM this month — it's usually a policy toggle, and it removes an entire breach category.

### PR-5 · PR.DS — Backups  *(priority)*
**Ask:** Are backups of critical data created on a schedule, protected from tampering (offline or immutable), and actually tested by restoring?
**Explain:** Backups are your ransomware survival plan — which is why ransomware operators hunt them first. Untested backups are a hypothesis; immutable/offline copies are the control.
**Tiers:** T1: no reliable backups of some critical systems. T2: backups run; restores untested; copies reachable from the domain. T3: 3-2-1 with an offline/immutable copy, restore tests on a schedule, coverage mapped to critical systems. T4: restore times measured against RTOs; backup integrity monitored; regular full-recovery exercises.
**Controls:** 3-2-1 rule; immutable/object-lock or offline copy; separate backup credentials (not domain-joined admin); quarterly restore test with evidence.
**If low:** This month: verify every critical system is actually in the backup set, create one copy ransomware can't reach, and restore one real system as a test.

### PR-6 · PR.PS — Secure configuration
**Ask:** Are systems deployed and maintained against hardened configuration baselines, with changes managed?
**Explain:** Defaults are built for setup convenience, not defense. Baselines (CIS Benchmarks, DISA STIGs) close the easy doors: default creds, open services, macro settings, legacy protocols.
**Tiers:** T1: default configs; snowflake servers. T2: informal build notes; drift unmeasured. T3: documented baselines (CIS/vendor) applied via policy/images, drift checked, change management in place. T4: configuration-as-code; drift auto-remediated; baselines updated from threat intel.
**Controls:** CIS Benchmarks / Microsoft security baselines via GPO/Intune; disable SMBv1/NTLMv1/legacy auth; standard server build; change advisory process.
**If low:** Apply the free CIS/Microsoft baseline to endpoints via GPO/Intune, and kill the classics first: SMBv1, legacy auth, Office macros from the internet.

### PR-7 · PR.PS — Patch & vulnerability remediation  *(priority)*
**Ask:** Are operating systems, applications, and firmware patched on defined timelines — including internet-facing systems on an accelerated one?
**Explain:** Most intrusions use vulnerabilities with patches already available. Internet-facing systems (VPN, mail, web) are scanned by attackers within hours of a CVE dropping — they need days-not-months timelines.
**Tiers:** T1: patching is manual and sporadic; unknown coverage. T2: OS patching automated; apps/firmware/edge devices lag. T3: defined SLAs (e.g., critical/internet-facing ≤14 days), automated deployment, coverage measured. T4: KEV-driven emergency process exercised; near-full coverage verified by scanning.
**Controls:** WSUS/Intune/RMM automated patching; app patching (browsers, Java, Adobe); firmware/appliance update process; patch compliance dashboard.
**If low:** Automate OS patching everywhere you can, and put internet-facing devices (VPN/firewall/mail) on a 14-day-or-faster rule tied to CISA KEV.

### PR-8 · PR.IR — Network segmentation & resilience
**Ask:** Is your network segmented so critical systems and risky zones (guest, OT/SCADA, legacy) are separated, and is infrastructure resilient to failure?
**Explain:** Flat networks turn one infected workstation into an agency-wide incident. Segmentation buys containment; redundancy (power, capacity, failover) buys uptime.
**Tiers:** T1: flat network; guest and business traffic mingle. T2: basic VLANs, permissive rules between them. T3: segmentation with enforced ACLs isolating critical systems/OT/guest; capacity and redundancy planned. T4: segmentation tested (pentest/purple team); micro-segmentation or zero-trust patterns for crown jewels.
**Controls:** VLANs + inter-VLAN firewall rules; isolate OT/SCADA and building systems; guest wireless isolation; deny-by-default between zones; UPS/failover for critical infrastructure.
**If low:** Start with three fences: guest wireless off the business network, servers separated from user endpoints, and any OT/legacy gear behind its own firewall.

---

## DETECT — 4 questions

### DE-1 · DE.CM — Logging coverage
**Ask:** Are security-relevant logs collected from your key sources — identity, endpoints, network/firewall, servers, and cloud services — and retained long enough to investigate?
**Explain:** You can't detect or investigate what you didn't record. Identity logs (sign-ins) and endpoint logs matter most; median breach discovery takes months, so retention of 90 days hot / 1 year total is a common floor.
**Tiers:** T1: default local logs only, overwritten quickly. T2: some sources centralized; big gaps (cloud, endpoints). T3: defined log sources covering identity/endpoint/network/cloud, centrally collected, retention set by policy. T4: coverage validated against detection needs (e.g., MITRE ATT&CK); gaps tracked.
**Controls:** Centralized syslog/agent collection; M365/Entra & cloud audit logs enabled and exported; EDR telemetry; retention standard.
**If low:** Turn on and centralize the two highest-value sources first: identity provider sign-in/audit logs and EDR telemetry.

### DE-2 · DE.CM — Continuous monitoring & alerting  *(priority)*
**Ask:** Is someone (or something) actually watching — analyzing those logs and endpoint telemetry and generating alerts a human responds to, including outside business hours?
**Explain:** Logs without eyes are a diary of your breach. Ransomware deploys at 2 a.m. on holiday weekends by design. Small shops meet this with managed detection (MDR/SOC-as-a-service) rather than staffing a SOC.
**Tiers:** T1: nobody reviews anything until an outage. T2: alerts exist, reviewed business hours, best effort. T3: EDR + monitored alerting with 24/7 coverage (in-house or MDR/MSSP), defined response times. T4: tuned detections, threat hunting, coverage tested with purple-team exercises.
**Controls:** EDR/XDR on all endpoints and servers; MDR service or SIEM with on-call; MS-ISAC Albert sensor (SLTT); WA agencies are also covered by the WaTech SOC's enterprise monitoring.
**If low:** If you can't watch 24/7, buy it: EDR + an MDR service is the fastest realistic path to around-the-clock detection for a small team.

### DE-3 · DE.AE — Event analysis & triage
**Ask:** When an alert or report comes in, is there a defined process to triage it — assess scope, severity, and whether it's real — rather than improvising?
**Explain:** Triage is the bridge between "weird alert" and "declared incident." Without it, real events get dismissed and false positives eat the week. Correlating across sources (that sign-in + that endpoint alert) is what turns noise into a finding.
**Tiers:** T1: alerts handled by gut feel, inconsistently. T2: informal triage by whoever's around; nothing recorded. T3: documented triage steps, severity levels, and correlation across sources; outcomes logged. T4: enriched/automated triage (SOAR, intel lookups); triage quality reviewed.
**Controls:** Alert triage runbook; severity matrix; ticketing of every security event; enrichment (VirusTotal, intel feeds).
**If low:** Write a one-page triage runbook: who assesses, the 5 questions they answer (what/where/who/real?/spreading?), and the severity ladder.

### DE-4 · DE.AE — Incident declaration criteria
**Ask:** Are there defined thresholds for declaring an incident — so it's clear when an event becomes an incident and who gets told?
**Explain:** The most expensive minutes of a breach are the ones spent debating whether it's "really an incident." Pre-agreed criteria remove hesitation and trigger the response plan, notifications, and clock-driven legal duties.
**Tiers:** T1: incidents declared by argument, usually late. T2: rough shared understanding, not written. T3: written criteria tied to severity levels, with who-declares and who-gets-notified defined. T4: criteria refined from real incidents/exercises; declaration times measured.
**Controls:** Incident severity/declaration matrix in the IR plan; auto-escalation rules for confirmed ransomware/data exposure; alignment with reporting duties (for WA state agencies, WaTech's SEC-10 incident policy).
**If low:** Add a half-page to your IR plan: 4 severity levels, examples of each, who can declare, and who is notified at each level.

---

## RESPOND — 5 questions

### RS-1 · RS.MA — Incident response plan  *(priority)*
**Ask:** Do you have a written incident response plan with assigned roles, current contact lists, and has it been exercised in the last year?
**Explain:** The IR plan is the script for your worst day. Untested plans fail in predictable ways: stale phone numbers, no one authorized to disconnect systems, no out-of-band comms when email is down. A tabletop exercise once a year is the minimum pulse check.
**Tiers:** T1: no plan, or a template nobody's read. T2: plan exists; roles fuzzy; never exercised. T3: current plan, named roles with backups, out-of-band contacts, annual tabletop with after-action. T4: exercised against realistic scenarios (ransomware, BEC); plan updated from every real incident.
**Controls:** IR plan (NIST SP 800-61 structure); printed/offline contact tree; annual tabletop (CISA offers free SLTT exercise support); cyber insurance and legal counsel contacts pre-listed.
**If low:** Adapt a template IR plan, fill in real names and phone numbers, print it, and run a 90-minute ransomware tabletop this quarter.

### RS-2 · RS.MA — Triage, categorization & escalation
**Ask:** During an incident, are events categorized and escalated on defined paths — including to leadership, legal, and third parties — with the plan actually followed?
**Explain:** Mid-incident is the wrong time to figure out who calls the director, when counsel gets looped in (privilege matters), or how to reach the vendor's security team. Escalation paths keep the response coordinated instead of heroic.
**Tiers:** T1: escalation is improvised phone tag. T2: people know roughly who to call; thresholds undefined. T3: severity-based escalation matrix incl. leadership/legal/vendors, followed and recorded during incidents. T4: escalation drilled and timed; coordination roles (incident commander) practiced.
**Controls:** Escalation matrix by severity; incident commander role; legal/comms engagement criteria; vendor security contacts on file.
**If low:** Build the escalation matrix into the IR plan: for each severity level, who's notified, by when, by whom.

### RS-3 · RS.AN — Investigation & evidence
**Ask:** Can you investigate an incident — determine root cause and scope — and preserve evidence (forensic images, logs, chain of custody) properly?
**Explain:** Investigation answers "how did they get in and what did they touch" — which determines legal notification duties and whether the hole gets fixed. Evidence handling matters if it goes to law enforcement, insurance, or court. Most agencies buy this via an IR retainer rather than staff it.
**Tiers:** T1: wipe-and-reimage, questions never answered. T2: basic log review by IT; evidence often destroyed by cleanup. T3: documented investigation procedures, evidence preservation steps, access to forensic capability (in-house or retainer). T4: mature forensics/DFIR capability, chain of custody routine, findings feed detection improvements.
**Controls:** Evidence preservation checklist ("isolate, don't wipe"); IR retainer or insurer's DFIR panel; log retention supporting look-back; WA CIRT / WaTech CIRT assistance.
**If low:** Two moves: put "preserve before you rebuild" in the IR plan, and line up outside forensic help *before* you need it (retainer, insurer panel, or the state).

### RS-4 · RS.CO — Notification & reporting
**Ask:** Do you know your incident reporting obligations — internal, to the state, to regulators, to affected individuals — with timelines, and are they built into your response process?
**Explain:** Reporting is law, not courtesy. Washington state agencies report incidents to the WaTech SOC/CIRT (360-407-8800); breach notification to individuals and the Attorney General runs on statutory clocks (RCW 19.255 / 42.56.590 — 30 days); sector rules (CJIS, HIPAA, IRS 1075) add their own. Missing a clock turns an incident into a second incident.
**Tiers:** T1: obligations unknown; would be researched mid-crisis. T2: someone knows most of them; not documented. T3: reporting matrix (who/what/when) in the IR plan, incl. state reporting and breach counsel; used in incidents/exercises. T4: notifications templated and rehearsed; regulator relationships established beforehand.
**Controls:** Reporting obligation matrix; WaTech SOC 360-407-8800 / SOC@watech.wa.gov (WA agencies); AG breach notification process; CISA/FBI IC3 reporting; pre-drafted notification templates.
**If low:** Build the one-page reporting matrix now — every obligation, trigger, deadline, and phone number — and staple it into the IR plan.

### RS-5 · RS.MI — Containment & eradication
**Ask:** Can you rapidly contain an incident — isolate hosts, disable accounts, block indicators — and fully eradicate the attacker's access before recovery?
**Explain:** Containment speed decides whether ransomware hits 3 machines or 300. Eradication is the unglamorous step people skip: rebuilding, rotating *all* credentials the attacker could have touched, and closing the entry point — otherwise they're back in a week.
**Tiers:** T1: containment = pulling cables if someone's there. T2: manual containment during business hours; eradication ad hoc. T3: EDR-based isolation and account-disable procedures usable 24/7; eradication checklist incl. credential rotation and entry-point fix. T4: containment automated for high-confidence detections; eradication verified by hunting before restoration.
**Controls:** EDR network-isolation capability; break-glass procedures to disable accounts/revoke sessions fast; ransomware playbook; full credential rotation (incl. krbtgt twice) post-compromise.
**If low:** Verify today that on-call staff can isolate any endpoint and disable any account within minutes, from home, at 2 a.m. — then write the eradication checklist.

---

## RECOVER — 4 questions

### RC-1 · RC.RP — Recovery execution
**Ask:** Do you have recovery procedures for critical systems — with recovery time objectives — and have you proven you can restore from backups at scale?
**Explain:** Recovery is where PR-5's backups meet reality. Restoring one file is not restoring a domain controller, a finance system, and 200 endpoints in dependency order while everything is on fire. RTOs set expectations leadership has agreed to in advance.
**Tiers:** T1: recovery would be invented live. T2: procedures for some systems; RTOs aspirational; never tested beyond single files. T3: documented recovery runbooks with RTO/RPO for critical systems, restoration order defined, tested at least annually. T4: full-scale recovery exercised (incl. from immutable copies); actual times measured against RTOs.
**Controls:** DR plan with RTO/RPO per critical system; restoration priority list; annual recovery exercise; documented rebuild procedures for identity infrastructure.
**If low:** Pick your single most critical system and do a timed full restore this quarter. The gap between assumed and actual recovery time is the finding.

### RC-2 · RC.RP — Integrity verification & prioritized restoration
**Ask:** Before and during restoration, do you verify backups/systems are clean and restore in a deliberate priority order?
**Explain:** The classic recovery failure is restoring the malware along with the data, or restoring apps before the identity/network services they depend on. Verification (scan backups, confirm eradication, check backup dates against dwell time) prevents round two.
**Tiers:** T1: restore everything as fast as possible, hope it's clean. T2: informal checks by whoever's restoring. T3: defined verification steps (clean-point selection, malware scanning, eradication confirmed) and a dependency-ordered restoration plan. T4: golden images, integrity monitoring, staged clean-room restoration practiced.
**Controls:** Restoration priority/dependency map; backup scanning; "clean point" determination in the IR process; rebuild-from-known-good for compromised identity systems.
**If low:** Add a checkpoint to the DR plan: no restoration begins until scope/eradication is confirmed and a clean restore point is chosen.

### RC-3 · RC.CO — Recovery communications (internal & stakeholders)
**Ask:** During an outage or recovery, can you communicate status to staff, leadership, and dependent partners — even if email and phones are down?
**Explain:** During ransomware, your comms channels may be encrypted along with everything else. Staff need to know what to do (and not do); leadership needs honest status; partner agencies relying on your services need warning. Out-of-band channels must be arranged in advance.
**Tiers:** T1: no plan; rumors fill the vacuum. T2: someone would send updates if systems allow. T3: comms plan with out-of-band channels (cell tree, alternate email, SMS service), defined cadence and spokespeople. T4: comms rehearsed in exercises; stakeholder maps maintained; status page ready.
**Controls:** Out-of-band communication method; internal status update cadence; pre-identified spokesperson; partner/stakeholder contact list.
**If low:** Set up one out-of-band channel now (text tree, Signal group, or external status page) and put it in the plan.

### RC-4 · RC.CO — Public updates & post-recovery review
**Ask:** Are public/press/affected-individual communications coordinated through defined channels, and does every significant incident end with a post-incident review?
**Explain:** For public agencies, incidents are public-records-adjacent news. Uncoordinated statements create legal exposure and erode trust; silence does too. And the incident isn't over until the review is done and its actions land in the improvement tracker (see ID-5).
**Tiers:** T1: whoever answers the phone talks to the press; no reviews. T2: PIO involved late; reviews happen for big ones only, informally. T3: public comms run through PIO/leadership with legal review; post-incident review standard, actions tracked. T4: holding statements pre-drafted; transparency posture decided in advance; review findings measurably close.
**Controls:** PIO engagement in the IR plan; pre-approved holding statements; AG-notification coordination; post-incident review template with tracked actions.
**If low:** Pre-draft two holding statements (service outage, data incident) with your PIO and legal now — mid-incident wordsmithing is how agencies end up on the news twice.
