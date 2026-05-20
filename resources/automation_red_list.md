# 🚦 Automation Red List — Before You Build Any Flow

Day 1's Red/Green list still applies. **Automation amplifies the risk.** A bad prompt is one wrong answer; a bad flow can send 500 wrong emails before you realise.

---

## 🛑 NEVER automate (full stop)

| Action | Why |
|--------|-----|
| Auto-sending external emails based on AI classification | One mis-classified email to a regulator can become a compliance event |
| Auto-posting to social media | Reputational risk is asymmetric and irreversible |
| Auto-approval of payments | Procurement/finance fraud risk; PPRA scrutiny |
| Auto-deletion of files based on AI judgement | "Permanent" actions need humans |
| Auto-publishing of incident reports | Pre-disclosure release is an OGRA Section 26 violation risk |
| Auto-acceptance of contracts or T&Cs | Legal commitments need a person, not a robot |
| Auto-forwarding of confidential email threads | Data leak risk; PECA 2016 exposure |
| AI-generated content sent without human review to anyone external | Hallucinations become company commitments |

---

## ⚠️ AUTOMATE WITH A HUMAN-IN-THE-LOOP CHECKPOINT

For these, build the flow but make it pause for a human approval before the consequential step:

- Drafting an email to a customer / vendor / regulator → AI drafts, human reviews, human sends
- Classifying an invoice for routing → AI suggests, finance officer confirms
- Tagging an HSE form by severity → AI scores, HSE officer signs off
- Extracting data from a contract → AI extracts, contracts officer verifies
- Generating a summary of a meeting → AI summarises, attendee approves before distribution
- Filing or categorising documents in SharePoint → AI proposes, owner accepts the move

**Pattern:** AI does the work; human owns the decision. Power Automate's "Approvals" action is built for exactly this.

---

## ✅ AUTOMATE FREELY

These have low risk of irreversible harm:

- Moving completed approval-ed documents into archive folders
- Sending **internal** notifications (you can fix mistakes)
- Generating draft documents stored in a "Drafts" folder (no auto-send)
- Logging events to an audit table
- Triggering reminder notifications to internal staff
- Backing up files between locations
- Renaming files based on metadata
- Posting internal Teams messages summarising completed work

---

## 🔄 The Five Automation Rules

1. **Reversibility first** — can you undo it? If no, add a human gate.
2. **Internal first, external later** — pilot inside your team for 30 days before any external-facing automation.
3. **Sample size matters** — a flow that runs 10 times has small blast radius; one that runs 10,000 times needs heavy testing.
4. **Audit log everywhere** — every automated decision must be logged with timestamp, input, output, and the AI confidence (where applicable).
5. **Kill switch ready** — every flow needs a "disable" button accessible to non-developers in case it misbehaves.

---

## 🚨 Pakistan-specific considerations

| Concern | Implication |
|---------|-------------|
| **PECA 2016** | Same as Day 1 — automated exfiltration of state-owned strategic data still attracts liability |
| **OGRA disclosure timing** | An automation that publishes incident data before regulatory disclosure window is a violation |
| **PPRA procurement rules** | Auto-approval of bids or BAFO acceptance is non-compliant with PPRA fairness rules |
| **State Bank circulars** | Auto-FX transactions or auto-payments above thresholds need manual sign-off |
| **Data residency** | Power Automate runs in your M365 tenant region (usually UAE/Singapore for Pakistan); confirm before sensitive flows |

---

## 🛡️ Pre-build checklist

Before clicking "Save" on any new flow, ask:

- [ ] Who can disable this if it misbehaves?
- [ ] What happens if it runs 1,000 times by accident?
- [ ] Are all destination addresses (emails, channels, recipients) on a test list first?
- [ ] Is there a human approval before any external send?
- [ ] Does the audit log capture inputs, outputs, and timestamps?
- [ ] Have I tested with mock data, not live data?
- [ ] Is there a "soft fail" — does it stop quietly if something looks wrong?

If you can't tick all seven, the flow is not ready for production. Test mode only.

---

## 🧪 Test-mode discipline

Every Power Automate flow has a **Run history** tab. **Always**:

1. Start with the trigger set to a test mailbox or test SharePoint list
2. Run at least 5 times with edge cases (empty fields, weird characters, non-English text)
3. Read every run's output in the history tab before promoting to production
4. Document what "production" looks like (which trigger, which recipients, which volume)
5. Set up alerts for failures — Power Automate emails you if a flow fails 3+ times

The Pakistani O&G engineer's instinct for "pre-job safety meeting before you do the dangerous thing" applies perfectly. **Test the flow before you trust the flow.**
