# 🧾 AI Document Reading — Invoice Extraction

**Time required:** 30–40 minutes
**Sample data:** [`sample_data/sample_invoice.txt`](sample_data/sample_invoice.txt)
**You will use:** AI Builder (Premium) **OR** Claude / ChatGPT (any tier)

---

## 🎯 What you will learn

1. Extract structured fields (vendor, amount, PO ref, line items, tax) from an invoice
2. Compare AI extraction confidence vs human verification
3. Feed extracted data into the Power Automate intake flow from Module 02

---

## 🛣️ Two paths to the same destination

### Path A — AI Builder in Power Automate (recommended for production)

1. `make.powerautomate.com` → **AI Builder → Models → + New AI model**
2. Choose **"Extract information from invoices"** — Microsoft's pre-built model
3. Test with `sample_invoice.txt` (or convert it to PDF first)
4. Review the extracted fields — vendor, total, line items
5. Use in a flow: **Trigger (new SharePoint file)** → **AI Builder: Process and save information from invoices** → **Use the extracted data downstream**

### Path B — Claude or ChatGPT (works for practice without AI Builder)

1. Open `claude.ai` or `chat.openai.com`
2. Start a fresh chat
3. Paste the contents of `sample_invoice.txt`
4. Use the structured extraction prompt below

---

## 🧪 Exercise — The Extraction Prompt (Path B)

Run this in Claude or ChatGPT:

```text
You are a finance automation assistant for a Pakistani O&G operator.

I am pasting an invoice (anonymised, fictional). Extract the following 
fields into a clean JSON object. If a field is missing or unclear, use 
null and add a note in the "uncertainties" array.

Fields:
- vendor_name
- vendor_taxid (if present)
- invoice_number
- invoice_date (YYYY-MM-DD)
- po_reference
- grn_reference (if present)
- currency
- subtotal
- tax_amount
- tax_rate_pct
- total_amount
- payment_terms_days
- bank_account (last 4 digits only)
- line_items (array of {description, quantity, unit_price, line_total})
- uncertainties (array of strings explaining any field that wasn't clear)
- confidence_overall (high / medium / low)

CONSTRAINTS:
- Do not invent any field. If absent, return null.
- Numbers as numbers, not strings.
- All currency amounts in the invoice's currency.

Invoice content:
[PASTE THE INVOICE HERE]
```

---

## 🧪 Exercise — Verify Before Trusting

After the extraction, **manually verify** at least three fields:

| Field | What to check |
|-------|---------------|
| `total_amount` | Add `subtotal` + `tax_amount`; does it match? |
| `line_items` total | Sum the line totals; does it equal `subtotal`? |
| `po_reference` | Open `[PASTE THE INVOICE HERE]` and Ctrl-F for the PO number; is it correctly captured? |
| `confidence_overall` | If the model says "low", treat the whole extraction as suspect |

**Always**: if `confidence_overall` is anything other than `high`, route to a human, not directly to payment.

---

## 🧪 Exercise — End-to-End Integration (Sketch)

For participants with AI Builder, build this:

1. **Trigger**: when a file is added to `SharePoint/Vendor Invoices Library` (from Module 02)
2. **AI Builder action**: "Process and save information from invoices" — output: JSON extraction
3. **SharePoint action**: create item in **Invoice Tracker** list with all extracted fields populated
4. **Condition**: is `total_amount` within ±2% of the corresponding PO?
5. **If yes** (good match): set `Status = Ready for Approval`; notify AP Supervisor
6. **If no** (mismatch): set `Status = Variance Investigation`; notify AP Clerk; include the variance amount in the notification
7. **Audit log**: every extraction logged with confidence, fields, and downstream decision

For participants without AI Builder: sketch the flow on paper — same logic, swap the AI Builder action for "send to Claude/ChatGPT via custom HTTP" (this is an advanced premium pattern; for now, use it as a thinking exercise).

---

## 🚨 Common failure modes (and how to handle them)

| Failure | Why it happens | Fix |
|---------|--------------|-----|
| Wrong vendor name | Logo image without text fallback | Use a "vendor lookup" against your master data, not what the AI extracted |
| Wrong currency | "PKR" vs "Rs" vs "Rupees" | Force a default if vendor master record specifies |
| Decimal/comma confusion | "1,234.56" vs "1.234,56" | Add a sanity check: anything above the PO value is suspect |
| Missing line items on multi-page invoice | OCR cut off on second page | Verify line count against page count |
| Tax mis-calculated | Vendor used wrong rate | Recompute tax from subtotal and rate; if mismatch, flag |
| Duplicate invoice processed | Same invoice arrives twice | Check Invoice Tracker for duplicate `invoice_number` before processing |

---

## 🎓 What you've unlocked

Once you can reliably extract structured data from invoices, you can apply the same pattern to:

- **HSE forms** — extracting fields from completed incident forms (next file in this module)
- **POs** — auto-classification for routing (also in this module)
- **Contracts** — clause extraction for review queues
- **Tender documents** — automated extraction of bidder details, prices, technical scores
- **Customs and trade docs** — for import/export workflows

Each follows the same recipe: **AI extracts → human verifies → flow routes.**

---

## ➡️ Next step

Move on to [`po_classification.md`](po_classification.md) for auto-classification techniques.
