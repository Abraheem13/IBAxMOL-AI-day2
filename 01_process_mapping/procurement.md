# 📦 Process Mapping — Procurement (PPRA Goods Purchase)

**Time required:** 30–40 minutes
**Sample data:** [`sample_data/procurement_process_steps.txt`](sample_data/procurement_process_steps.txt)
**Deliverable:** One SIPOC + one swim-lane diagram on paper or whiteboard

---

## 🎯 What you will learn

1. Map a routine PPRA-compliant goods-purchase request from raise to receipt
2. Identify the 3 highest-value automation candidates in the process
3. Distinguish automation candidates from process-redesign candidates

---

## 🧪 Exercise 1 — Build the SIPOC

**Setup:** Open [`sample_data/procurement_process_steps.txt`](sample_data/procurement_process_steps.txt) and read the 18 process steps end-to-end.

**On paper, draw five columns:**

| Suppliers | Inputs | Process | Outputs | Customers |
|-----------|--------|---------|---------|-----------|
| | | | | |

**Fill in:**

- **Suppliers**: who feeds the process? (Requesting department, vendors, finance, etc.)
- **Inputs**: what arrives? (Purchase requisition, technical spec, budget approval)
- **Process**: 5–7 high-level steps (not all 18 — keep this view "executive")
- **Outputs**: what leaves? (Approved PO, delivered goods, GRN, payment)
- **Customers**: who receives the outputs? (Requesting department, finance, vendor, audit)

**The trap to avoid:** putting all 18 steps in the "Process" column. SIPOC is the 30,000-ft view. Save the detail for the swim-lane.

---

## 🧪 Exercise 2 — Build the Swim-Lane

**On paper or in PowerPoint, draw a swim-lane with these rows:**

1. Requesting Department
2. Procurement Officer
3. Finance / Budget Holder
4. Procurement Committee
5. Vendor
6. Stores / Warehouse
7. SAP / ERP system

**Place each of the 18 steps** in the row where it actually happens. Use arrows to show handoffs between rows.

**Then mark the friction with red ink:**

- 🔴 Wherever a step waits more than 24 hours for the next one
- 🔴 Wherever the same person does the same approval twice in different formats
- 🔴 Wherever someone copies data from email into SAP by hand
- 🔴 Wherever a step depends on an Excel that lives outside SAP

---

## 🧪 Exercise 3 — Score Automation Candidates

For each friction point you marked, score it on this matrix:

| Friction step | Frequency (per month) | Avg time per occurrence | Total time saved/month | Risk if automated badly |
|---------------|-----------------------|-------------------------|------------------------|-------------------------|
| Step 3: Manager approval reminder follow-ups | ~25 | 15 min | 6.25 hours | Low — internal reminder |
| Step 8: Comparative statement preparation | ~15 | 90 min | 22.5 hours | Medium — must be accurate |
| Step 11: PO email to vendor + read-receipt chase | ~15 | 20 min | 5 hours | Low — internal nudge |
| Step 14: GRN cross-check vs PO | ~12 | 45 min | 9 hours | Medium — finance impact |
| Step 16: Invoice 3-way match | ~12 | 60 min | 12 hours | High — payment impact |

**The candidates to pursue:**
- **Step 3** — pure win, low risk, build it in Power Automate this week
- **Step 8** — clear win but needs spec careful testing
- **Step 16** — highest time saver, but **needs a human gate** (Red List rule)

---

## 🎓 What to take away

After this exercise:

1. **Not every friction is an automation candidate.** Some are process-redesign candidates (e.g., why do we need a Manager AND a Director approval for ₨ 50,000? Fix the policy, not just automate the dual-approval.).
2. **High-frequency, low-risk wins first.** Build confidence in your team with quick reminders and routing flows.
3. **The 3-way match is the killer use case** — but it must have a human signing off the actual release.
4. **Your swim-lane is the spec.** Hand it to your IT team or the Power Automate course tomorrow; they will build from this directly.

---

## 🤔 Common questions

**Q: Should I include the "informal" Excel my team uses?**
A: Yes. Map what *actually* happens, not what *should* happen. If shadow Excel exists, that's the most important thing on the map.

**Q: My process has 40+ steps. Is that normal?**
A: Possibly. But often what looks like 40 steps is 12 real steps with 28 sub-checks. Group sub-checks under the parent step.

**Q: What if my process varies depending on amount, vendor, or urgency?**
A: Map the **most common path** (the "happy path") in detail. Then add 1-2 "exception path" annotations. Don't try to capture every variant in the main diagram.

**Q: My boss wants to automate "the whole thing." What do I say?**
A: Bring this diagram. Show the three highest-value candidates and ask: "If we do these three this quarter, here's how much time we save. Should we do them, or should we attempt all 18 at once and probably fail?"

---

## ➡️ Next step

Move on to [`hse.md`](hse.md), [`maintenance.md`](maintenance.md), or [`finance.md`](finance.md) — or jump to [`../02_power_automate/`](../02_power_automate/) to start building.
