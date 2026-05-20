# Module 03 — AI-Powered Document Reading & Classification

**Why this module matters:** Most O&G operators are drowning in unstructured documents — invoices arriving as PDFs, HSE forms as scanned images, POs in inconsistent formats, contracts in dozens of templates. This module teaches you to turn that chaos into structured data your automations can act on.

---

## 📦 Sub-modules

| File | What you'll learn |
|------|---------------------|
| [`invoice_extraction.md`](invoice_extraction.md) | Extract vendor, amount, PO reference, line items from invoice PDFs |
| [`po_classification.md`](po_classification.md) | Auto-classify incoming POs by category, urgency and approval level |
| [`hse_form_extraction.md`](hse_form_extraction.md) | Pull structured fields from completed HSE incident forms |

---

## 🧭 The two AI-document approaches

| Approach | When to use | Tools |
|----------|------------|-------|
| **AI Builder in Power Automate** | Document arrives via your tenant; result feeds another flow | AI Builder (Premium) inside Power Automate |
| **Public LLM (ChatGPT / Claude) via API or copy-paste** | One-off review, anonymised data, lower volume | ChatGPT, Claude — with anti-hallucination prompts |

**Day 2 focuses primarily on the first** — the in-tenant, in-flow approach — because it composes with the Power Automate flows you built in Module 02. For higher-volume needs and live data, AI Builder + Power Automate is the right architecture.

For practice without an AI Builder licence, you can run the same prompts in ChatGPT or Claude using anonymised sample documents.

---

## ⚠️ Setup considerations

- **AI Builder licence** is a Premium add-on to Power Automate. Confirm with IT before pursuing the in-flow path.
- **Sample documents** in this module are fictional and safe to upload to public AI for the copy-paste approach.
- **Real documents** stay on the Red List — anonymise heavily before any public-AI use.

---

## ✅ Pre-flight checklist

- [ ] You completed Module 02 (Power Automate basics)
- [ ] You have read [`resources/automation_red_list.md`](../resources/automation_red_list.md)
- [ ] You know whether your account has AI Builder access (ask IT)
- [ ] You have a backup browser tab open to `claude.ai` for the no-AI-Builder path

---

## 🎓 Learning outcomes

By the end of this module you will:

1. Use AI Builder to extract structured fields from an invoice PDF (or simulate the same with Claude)
2. Classify incoming documents by type, urgency, and routing destination
3. Combine document extraction with Power Automate flows — end-to-end automation
4. Recognise the limits of AI document reading — and where humans must stay in the loop

---

## 🔥 The killer use case

Combining **Module 02 + Module 03**:

```
Invoice arrives → Outlook trigger fires → 
PDF saved to SharePoint → AI Builder extracts fields → 
Power Automate checks vs PO and GRN → 
If match: route to AP supervisor for approval → 
If mismatch: flag for AP clerk investigation → 
Approved: payment list updated → audit log entry
```

This is the pattern you will see in **Aramco's Metabrain, ADNOC's ENERGYai, and Shell's procurement transformation projects**. It's no longer experimental. It's standard.

---

## 🚨 The non-negotiables

| Action | Status |
|--------|--------|
| AI extracts data | ✅ Automate |
| AI classifies (with confidence score) | ✅ Automate |
| AI flags exceptions for human review | ✅ Automate |
| AI auto-routes low-risk items | ⚠️ Only with confidence threshold + audit log |
| AI auto-approves payments | 🛑 NEVER — Treasury / Finance Manager signs |
| AI auto-files OGRA disclosures | 🛑 NEVER — HSE Manager signs |
| AI auto-submits bids | 🛑 NEVER — Procurement Committee decides |

Same line as Day 1: **drafts and pre-checks automate; final decisions stay human.**
