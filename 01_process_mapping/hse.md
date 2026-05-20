# 🦺 Process Mapping — HSE Incident Notification

**Time required:** 30–40 minutes
**Sample data:** [`sample_data/hse_incident_workflow.txt`](sample_data/hse_incident_workflow.txt)
**Deliverable:** SIPOC + swim-lane for incident intake → OGRA Section 26 disclosure

---

## 🎯 What you will learn

1. Map an HSE incident from field-discovery to regulatory disclosure
2. Identify the time-critical steps (OGRA 48-hour window)
3. Recognise where automation helps reaction time vs. where it would create disclosure risk

---

## 🧪 Exercise 1 — SIPOC

Read [`sample_data/hse_incident_workflow.txt`](sample_data/hse_incident_workflow.txt). Then draw your five columns.

**Trap to avoid:** in HSE, "customers" includes both internal (GM Operations) AND external (OGRA, PEPA, neighbouring communities). Capture both.

**Suggested fill:**

| Suppliers | Inputs | Process | Outputs | Customers |
|-----------|--------|---------|---------|-----------|
| Field operator · Control room · Contractor | Verbal alert · Gas detector reading · Eyewitness account | 1. Initial response · 2. Containment · 3. Investigation · 4. Reporting · 5. Disclosure · 6. CAPA tracking | Incident report · OGRA Section 26 filing · CAPA log · Lessons learned | GM Ops · HSE Director · OGRA · PEPA · Insurer · Board |

---

## 🧪 Exercise 2 — Swim-Lane

Rows for the HSE process:

1. Field Operator / Shift Supervisor
2. Control Room
3. HSE Officer (on-site)
4. HSE Manager
5. GM Operations
6. Compliance / Legal
7. OGRA (external)
8. Internal incident system (e.g., SAP, ProcessSafetySys)

**The critical timing markers to draw on your diagram:**

| Step | Window |
|------|--------|
| Initial verbal escalation | < 5 minutes |
| HSE Officer on-site | < 30 minutes |
| Internal incident form initiated | < 4 hours |
| GM Operations briefed | < 8 hours |
| Internal investigation kick-off | < 24 hours |
| **OGRA Section 26 disclosure** | **< 48 hours** (per regulation) |
| CAPA plan drafted | < 7 days |
| Lessons-learned brief circulated | < 14 days |

---

## 🧪 Exercise 3 — Where automation helps (and where it doesn't)

| Step | Automation candidate? | Why / why not |
|------|----------------------|---------------|
| Initial verbal escalation | ❌ No | Human judgement and speed beats any system |
| Notify ICR (immediate-care responders) of severity | ✅ YES | A form submission can trigger Teams alerts + SMS in seconds |
| Start a 48-hour OGRA countdown timer | ✅ YES | Automated reminders to HSE Manager at 24h, 36h, 44h |
| Draft OGRA disclosure | ⚠️ HUMAN-IN-LOOP | AI drafts, HSE Manager signs |
| **Submit** OGRA disclosure | 🛑 NEVER auto-submit | A draft must be reviewed; submission is irrevocable |
| CAPA action reminders to owners | ✅ YES | Pure win — recurring nudges |
| Lessons-learned circulation | ✅ YES | Once approved, automate the email/SharePoint posting |

---

## 🚨 The single most important rule for HSE automation

> **Drafts can be automated. Submissions to a regulator cannot.**

OGRA disclosures, PEPA notifications, and any regulator-facing filing must have a named human sign-off. Power Automate's "Approvals" action is perfect: AI drafts, the flow pauses for approval, the approval is logged, the submission is then released to the human to send manually.

**Why manual final-send?** Because the human's email, sent from their account, creates the personal accountability that regulators expect. An automated send blurs ownership.

---

## 🤔 Common questions

**Q: What about an automatic SMS to all senior management within 5 minutes of a Category 1 incident?**
A: Yes — internal notifications are appropriate to automate. Internal-only, internal-only, internal-only.

**Q: Can we automate the press release for major incidents?**
A: No. Press releases are board-approved. Draft them with AI, sign them by hand.

**Q: What about automatic incident categorisation (Cat 1, Cat 2, Cat 3)?**
A: AI can suggest a category based on severity criteria; HSE Manager confirms. Never auto-finalise.

**Q: We need OGRA notifications faster. Can the flow auto-submit?**
A: No. The 48-hour window is generous for a reason — it gives you time to verify. Speed for speed's sake creates compliance risk. Automate the **draft preparation** to within 4 hours instead.

---

## 🎓 What to take away

1. Time-critical processes benefit massively from automation — for **reminders, routing, drafting, and notifications**.
2. **Regulator submissions stay manual.** This is the line.
3. Build the 48-hour countdown timer this quarter. It's a 30-minute Power Automate flow that may save your career.

---

## ➡️ Next step

Continue with [`maintenance.md`](maintenance.md), [`finance.md`](finance.md), or jump to [`../02_power_automate/`](../02_power_automate/).
