# 📑 AI Document Reading — PO Classification

**Time required:** 25–35 minutes
**Sample data:** [`sample_data/sample_po.txt`](sample_data/sample_po.txt)
**You will use:** Claude or ChatGPT (free tier OK) — and Power Automate for routing

---

## 🎯 What you will learn

1. Classify incoming PO documents by category, urgency, and approval level
2. Generate routing decisions the Power Automate flow can act on
3. Identify edge cases that need human review

---

## 🧪 Exercise 1 — The Classification Prompt

Open `claude.ai` or `chat.openai.com`. Paste the sample PO:

```text
You are a procurement automation assistant for a Pakistani O&G operator.

I am pasting a Purchase Order. Classify it into the following dimensions 
and return a clean JSON object:

DIMENSIONS:
1. category: one of [
     "stationery_consumables",
     "ppe_safety",
     "spare_parts_mechanical",
     "spare_parts_electrical",
     "spare_parts_instrumentation",
     "chemicals_lubricants",
     "services_routine",
     "services_specialised",
     "it_software_hardware",
     "civil_works",
     "fuel_energy",
     "other"
   ]

2. urgency: one of [
     "routine" (normal cycle),
     "expedited" (operational need within 7 days),
     "emergency" (safety/production critical within 24-48 hours)
   ]

3. approval_level_required: one of [
     "department_head_only",
     "department_head_plus_finance",
     "department_head_plus_finance_plus_director",
     "exec_committee_required"
   ]

   Approval thresholds (in PKR):
   - up to 100,000 — department_head_only
   - 100,001 to 1,000,000 — department_head_plus_finance
   - 1,000,001 to 5,000,000 — department_head_plus_finance_plus_director
   - above 5,000,000 — exec_committee_required

4. routing_destination: name of the function to which this PO should be routed
   for technical evaluation (e.g., "Maintenance Engineering",
   "HSE Department", "Procurement Officer Routine").

5. potential_red_flags: array of strings — anything that warrants human review
   (e.g., "vendor not on approved list", "unusual delivery terms", 
   "round-number total suggests manual entry", "split PO to stay under 
   threshold pattern", "no specifications attached").

6. confidence: high / medium / low — your overall confidence in this 
   classification.

CONSTRAINTS:
- Use only the dimensions and values listed above.
- If a field is unclear, mark confidence as "medium" or "low" and explain in red_flags.
- Do not invent fields. JSON only, no prose explanation.

PO content:
[PASTE THE PO HERE]
```

---

## 🧪 Exercise 2 — Edge Case Detection

After classification, ask Claude or ChatGPT this follow-up:

```text
Now examine this PO again for the following procurement risk patterns. 
For each, answer with one sentence — "Detected: <evidence>" or "Not detected":

1. Splitting: is the amount suspiciously close to (but below) an approval threshold?
2. Single-source: is the vendor referenced as if no competition occurred?
3. Round-number anomaly: are the line totals suspiciously rounded?
4. Off-template: does this PO deviate from a standard format?
5. Missing references: are PO number, GRN ref, contract ref present and consistent?
6. Date inconsistencies: do the issue date, delivery date, and contract date make sense?
7. Vendor flag: is the vendor name unfamiliar (you can say "requires master data check")?

Conclude with a recommendation: "Proceed normally" / "Route for additional review" / 
"Block pending procurement officer review".
```

This is the kind of pattern detection that AI is genuinely good at — surfacing things a human reading 200 POs/week would miss.

---

## 🧪 Exercise 3 — Use in a Power Automate Flow

Sketch this flow:

1. **Trigger**: new PO PDF saved to `SharePoint/Incoming POs Library`
2. **AI extraction**: call Claude or ChatGPT (via custom HTTP) **or** use AI Builder
3. **Parse JSON**: extract category, urgency, approval level, red flags
4. **Condition: any red flags?**
   - **Yes** → SharePoint Status = "Needs Review"; notify Procurement Officer
   - **No** → continue
5. **Switch on `approval_level_required`**:
   - `department_head_only` → start single approval
   - `department_head_plus_finance` → start dual approval
   - `department_head_plus_finance_plus_director` → start triple approval
   - `exec_committee_required` → flag for Procurement Committee meeting
6. **Switch on `urgency`**:
   - `emergency` → set approval timeout to 4 hours; SMS notifications enabled
   - `expedited` → 24-hour timeout
   - `routine` → 5-day timeout
7. **Audit log**: every classification logged with confidence, red flags, routing decision
8. **Human override**: a "Reclassify" button in SharePoint that any procurement officer can click

---

## 🚨 Where humans must stay in the loop

| Decision | Auto? |
|----------|-------|
| Category labelling | ✅ Auto with confidence > 0.85; human verifies < 0.85 |
| Urgency classification | ✅ Auto |
| Approval routing | ✅ Auto |
| **Red-flag handling** | 🛑 Always human review |
| Override of AI classification | ✅ Always human |
| **Final approval to release the PO** | 🛑 Human (this is PPRA-compliant requirement, not just policy) |

---

## 🎓 What this unlocks

A medium operator processing 150 POs/month, with each previously taking ~25 minutes to classify and route manually, saves **~62 hours/month** with this pattern.

Even better: the **red-flag detection** can catch fraud or split-procurement patterns that no human reviewer can spot at volume.

---

## ➡️ Next step

Move on to [`hse_form_extraction.md`](hse_form_extraction.md) — extracting structured fields from incident forms.
