# Module 01 — Process Mapping for Oil & Gas

**Why this module matters:** You cannot automate what you cannot describe. Most failed RPA projects fail because the team automated a *bad* process instead of fixing it first. This module gives you two reliable notations — **SIPOC** and **swim-lane** — so you can map any process clearly enough to either fix it or hand it to a developer.

---

## 📦 Sub-modules

| File | Function |
|------|----------|
| [`procurement.md`](procurement.md) | A PPRA-compliant goods-purchase request, end-to-end |
| [`hse.md`](hse.md) | Incident report intake and OGRA Section 26 notification |
| [`maintenance.md`](maintenance.md) | Work-order request to completion |
| [`finance.md`](finance.md) | Vendor invoice receipt to payment release |

Pick the one matching your function first; explore the others to see common patterns.

---

## 🧩 The two notations you need

### SIPOC — for the 30,000-ft view

**S**uppliers → **I**nputs → **P**rocess → **O**utputs → **C**ustomers

Use SIPOC when:
- You are scoping a process for the first time
- You need executive buy-in on what's in/out of scope
- You haven't decided yet whether to automate, redesign, or delete

### Swim-lane — for the developer-ready view

Rows = roles or systems (Procurement Officer / SAP / Vendor / Bank). Columns = time. Steps appear in the right lane at the right time.

Use swim-lane when:
- You're about to build a Power Automate flow
- You need to find handoff delays (where work sits between roles)
- You're presenting to IT for an automation request

**You will produce both for the same process** in the lab exercises.

---

## ✅ Pre-flight checklist

- [ ] You have read [`resources/automation_red_list.md`](../resources/automation_red_list.md)
- [ ] You have **paper and a pen** — yes, really. Map on paper first; software second.
- [ ] You have access to a digital whiteboard tool (optional: Miro, Lucidchart, or just PowerPoint with SmartArt)
- [ ] You have **a real process in mind** from your function — choose now

---

## 🎓 Learning outcomes

By the end of this module you will:

1. Produce a SIPOC for any process in under 15 minutes
2. Convert that SIPOC into a swim-lane diagram developers can build from
3. Identify the **3-5 highest-value automation opportunities** in a 10-step process
4. Spot the four classic anti-patterns: rework loops, ping-pong handoffs, swivel-chair work, and shadow Excel

---

## 🛠️ The 5-step process-mapping protocol

Use this same protocol for every process you map:

| Step | What you do | Time |
|------|-------------|------|
| 1 | **Walk the process** — talk to the people who actually do it, not just the manager | 30 min |
| 2 | **Draft SIPOC on paper** — keep it scrappy; you'll redo it | 10 min |
| 3 | **Convert to swim-lane** — add roles/systems as rows, steps as boxes | 20 min |
| 4 | **Mark the friction** — circle every handoff delay, rework loop, manual data re-entry | 5 min |
| 5 | **Score automation candidates** — for each marked friction, score: frequency, time saved, risk | 10 min |

Total: ~75 minutes for any process. Faster than you think.

---

## 🔍 The four anti-patterns to watch for

These are where automation lives:

1. **Rework loops** — a step that gets rejected and bounced back. (E.g., "submit invoice → rejected for missing PO → resubmit"). Automate the pre-check.
2. **Ping-pong handoffs** — same email going Officer → Manager → Officer → Manager three times. Automate the routing logic.
3. **Swivel-chair work** — a person copies data from System A into System B by hand. Build a connector.
4. **Shadow Excel** — a process officially uses SAP but everyone really tracks it in a private Excel. Either kill the Excel or make it the official tool.

Spot one of these and you have an automation candidate. Spot four in the same process and you have a major Day-2 win.
