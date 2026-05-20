# 💰 Process Mapping — Vendor Invoice to Payment

**Time required:** 30–40 minutes
**Sample data:** [`sample_data/finance_invoice_flow.txt`](sample_data/finance_invoice_flow.txt)
**Deliverable:** SIPOC + swim-lane for invoice intake → payment release

---

## 🎯 What you will learn

1. Map vendor-invoice receipt to payment release end-to-end
2. Find the **3-way match** as the highest-value AI-assisted automation
3. Recognise the State Bank / FBR touchpoints that must stay manual

---

## 🧪 Exercise 1 — SIPOC

Read [`sample_data/finance_invoice_flow.txt`](sample_data/finance_invoice_flow.txt). Build your SIPOC.

**Suggested fill:**

| Suppliers | Inputs | Process | Outputs | Customers |
|-----------|--------|---------|---------|-----------|
| Vendor · Procurement · Receiving · Project | Invoice · PO · GRN · Tax certificate | 1. Receive · 2. Match · 3. Approve · 4. Tax · 5. Release · 6. Reconcile | Approved payment · Tax filing · Posted entry · Vendor remittance advice | Vendor · FBR · Treasury · GL accounting |

---

## 🧪 Exercise 2 — Swim-Lane

Rows for the finance process:

1. Vendor
2. AP (accounts payable) Clerk
3. AP Supervisor
4. Budget Holder / Project Manager
5. Finance Manager
6. Treasury
7. Bank
8. SAP / ERP

**Friction to mark in red:**

- 🔴 Step 2: Invoice arrival format — PDF, paper, email body, sometimes WhatsApp photo
- 🔴 Step 3: PO + GRN + Invoice 3-way match — manually compared on screen
- 🔴 Step 5: Withholding tax determination — manual lookup of vendor category
- 🔴 Step 7: Budget-holder approval delay — emails sit unanswered for days
- 🔴 Step 10: Bank file generation — Excel exported, formatted, uploaded
- 🔴 Step 12: Vendor remittance advice — manually composed and sent

---

## 🧪 Exercise 3 — Automation candidates

| Friction | Frequency / month | Time saved if automated | Risk level |
|----------|------------------|------------------------|------------|
| Step 2: Invoice intake normalisation | ~400 | 10 min each = 67h | Low (drafting only) |
| Step 3: 3-way match | ~400 | 8 min each = 53h | **High — human gate required** |
| Step 5: WHT category lookup | ~400 | 3 min each = 20h | Medium |
| Step 7: Budget-holder reminder | ~200 | 5 min each = 17h | Low |
| Step 10: Bank file generation | ~10 | 2 hours each = 20h | **HIGH — Treasury sign-off required** |
| Step 12: Remittance advice | ~400 | 4 min each = 27h | Low |

**The killer use case for finance:** AI-assisted invoice intake + 3-way match suggestion. Saves ~120 hours/month for a medium operator. **Must** have human approval at the payment-release gate.

---

## 🚨 The State Bank and FBR considerations

| Touchpoint | Manual or auto? |
|------------|-----------------|
| Withholding tax determination | AI suggests, human confirms |
| Payment file submitted to bank | **Manual only** — Treasury accountability |
| FBR / SECP filings | **Manual only** — director accountability |
| FX conversion above threshold | **Manual only** — State Bank circular compliance |
| Vendor remittance advice (after release) | ✅ Automate |
| GL posting (after payment) | ✅ Automate |

The pattern is the same as HSE: **drafts and pre-checks automate; submissions stay manual.**

---

## 🤔 Common questions

**Q: Can AI fully automate the 3-way match?**
A: It can do 95% of the work — extracting amounts, matching line items, flagging variances. But the **release** must be a human action. Build the AI to a "ready to release" status; finance officer clicks the button.

**Q: What about invoices with errors (wrong amount, wrong currency, missing line)?**
A: AI flags them with a confidence score. High-confidence matches → routed to one queue. Anything ambiguous → routed to the AP supervisor for resolution. This is "exception-based handling" and is the single biggest finance productivity unlock.

**Q: Our small vendors send paper invoices. Can we still automate?**
A: Yes — scan and OCR them. AI document reading (Module 03) handles paper. The savings are biggest on these because manual data entry is most painful.

**Q: What about fraud risk?**
A: A well-designed flow REDUCES fraud risk because every step is logged. The risk increases when the human-in-the-loop is bypassed. Never remove the human gate.

---

## 🎓 What to take away

1. **AP is the highest-ROI function for automation** in most O&G operators. Hundreds of invoices/month each touched 5-7 times manually.
2. **Build a robust intake layer first** — once invoices are structured data in SAP, the rest follows.
3. **The 3-way match is the killer app.** Get this right and the finance team becomes a beat ahead.
4. **Releases stay manual. Always.** State Bank and FBR accountability is non-negotiable.

---

## ➡️ Next step

Move to [`../02_power_automate/`](../02_power_automate/) and start building.
