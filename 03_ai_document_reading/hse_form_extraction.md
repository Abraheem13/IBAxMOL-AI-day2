# 🦺 AI Document Reading — HSE Form Extraction

**Time required:** 25–35 minutes
**Sample data:** [`sample_data/sample_hse_form.txt`](sample_data/sample_hse_form.txt)
**You will use:** Claude or ChatGPT — and Power Automate for routing

---

## 🎯 What you will learn

1. Extract structured fields from a completed HSE incident form
2. Auto-classify severity and trigger time-sensitive workflows
3. Route forms to the correct destinations while keeping humans in the regulatory loop

---

## 🧪 Exercise 1 — The Structured Extraction Prompt

Paste the sample HSE form into Claude:

```text
You are an HSE document automation assistant for a Pakistani O&G operator.

I am pasting a completed incident form (anonymised, fictional). Extract 
the following fields into a clean JSON object. Use placeholders or null 
for missing data — never invent.

FIELDS:
- incident_id (if present)
- incident_datetime (ISO format)
- site_location
- reporting_supervisor_role (not name — role only, e.g., "Shift Supervisor")
- severity_self_classified (Category 1 / 2 / 3 / Near-Miss)
- people_affected_count
- injury_type (if any, otherwise null)
- environmental_release (true / false; if true, brief description)
- equipment_involved (anonymised, e.g., "Tank T-104")
- immediate_actions_taken (array of one-line bullets)
- witnesses_count
- contractors_involved_count
- ogra_section_26_potentially_triggered (yes / no / unsure — with reasoning)
- pepa_notification_potentially_triggered (yes / no / unsure)
- recommended_internal_distribution (array of roles)
- ai_severity_recommendation: re-classify the severity based on the description 
  alone — return Category 1 / 2 / 3 / Near-Miss
- ai_severity_reasoning: one sentence justifying the AI's severity call
- discrepancy_with_self_classification: true / false (is there a mismatch?)
- confidence (high / medium / low)
- uncertainties (array of strings)

CRITICAL CONSTRAINTS:
- Do NOT invent any names, dates, quantities, regulations, or section numbers.
- If a field is unclear, use null and note in uncertainties.
- If OGRA/PEPA triggering is unclear, default to "unsure" and explain.
- This is a draft for human review — never the final regulatory call.

Form content:
[PASTE THE HSE FORM HERE]
```

---

## 🧪 Exercise 2 — Severity Reconciliation

The most powerful use of AI on HSE forms is **severity verification**.

Run a follow-up:

```text
The supervisor classified this incident as Category 3 (minor near-miss). 
Based ONLY on what's described in the form, do you agree?

Return:
1. Agreement: "Agree" / "Suggest higher" / "Suggest lower" / "Insufficient information"
2. Reasoning: one paragraph
3. Evidence in the form: 2-3 direct excerpts that support your call
4. Recommended next action: what should the HSE Manager do in the next 4 hours?
```

Where AI says "Suggest higher" — that's the most valuable output of the entire day. **Always review** these cases manually within the first 4 hours.

---

## 🧪 Exercise 3 — End-to-End Flow Sketch

Build (or sketch on paper) this Power Automate flow:

1. **Trigger**: form is submitted via Microsoft Forms (HSE field form) OR PDF emailed to `hse-intake@[operator].com.pk`
2. **AI extraction**: AI Builder (or HTTP call to Claude) extracts the JSON above
3. **Parse JSON**
4. **Create item** in SharePoint **Incident Tracker** list with all extracted fields
5. **Branch on `ai_severity_recommendation`**:
   - **Category 1** → SMS + Teams alert to GM Operations, HSE Director within 5 minutes; **start the 48-hour OGRA countdown timer**
   - **Category 2** → Email + Teams notification to HSE Manager within 30 minutes
   - **Category 3 / Near-Miss** → Standard 4-hour notification to HSE Officer
6. **If `discrepancy_with_self_classification` is true**:
   - Flag for HSE Manager mandatory review
   - Include both classifications and AI reasoning in the notification
7. **If `ogra_section_26_potentially_triggered` is "yes" or "unsure"**:
   - Start the OGRA-disclosure-prep workflow (AI drafts → human signs)
   - Countdown timer at 24h, 36h, 44h marks
8. **Audit log**: every step logged

**Critical reminder:** the OGRA disclosure DRAFT is automated. The SUBMISSION is manual — HSE Manager hits send.

---

## 🚨 Edge cases the AI will struggle with

| Case | Why AI struggles | How to handle |
|------|-----------------|----------------|
| Form filled in Urdu | LLMs are weaker on Urdu technical vocabulary | Pre-translate; or restrict AI use to English forms |
| Handwritten form scanned to PDF | OCR quality varies | Use AI Builder's image extraction; verify low-confidence fields manually |
| Same person reports multiple incidents in one form | Confuses extraction | Split into separate forms before AI processing |
| Ambiguous severity language ("could have been serious") | Subjective | Always route to human review when AI confidence is medium or low |
| Cultural/regional terms | LLMs may not know "katcha pipeline" or local equipment names | Build a glossary file and inject as context |

---

## 🎓 What you've unlocked

This pattern applies to:

- **Near-miss reports** — typically high volume, ripe for auto-classification
- **Permit-to-work forms** — extract scope, hazards, controls, signatures
- **Toolbox talk records** — extract topic, attendees, date
- **Daily HSE checklists** — extract any "fail" findings for immediate routing
- **Audit findings reports** — extract findings, severities, owners, target dates
- **Contractor pre-job risk assessments** — extract risks, controls, sign-offs

Same shape, different forms.

---

## 🏆 Module 03 complete

You have now:
- Built three Power Automate flows
- Mapped processes in four functions  
- Extracted structured data from invoices, POs and HSE forms

Time for the capstone in [`../activities/activity_capstone.md`](../activities/activity_capstone.md).
