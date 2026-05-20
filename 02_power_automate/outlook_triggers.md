# 📧 Power Automate — Outlook-Triggered Automations

**Time required:** 30–40 minutes
**You will build:** An email-trigger flow that auto-files vendor invoice attachments

---

## 🎯 What you will build

A flow that:
1. Triggers when a new email arrives in a specific folder (e.g., `Inbox/Vendor Invoices`)
2. Checks if the email has attachments
3. Saves each attachment to a SharePoint document library (or OneDrive)
4. Extracts the subject, sender, and date into a SharePoint tracking list
5. Posts a notification to your Finance team's Teams channel
6. Marks the email as read and applies a Category flag

This is the gateway to AI-powered document reading (Module 03) — you're building the **intake layer**.

---

## 🧭 Step-by-step build

### Phase 1 — Prepare the Outlook folder (3 min)

1. In Outlook (web or desktop): create a new folder under Inbox called `Vendor Invoices`
2. Set up an Outlook rule to move incoming invoice emails to this folder (or do it manually for testing)

> The folder is your "intake channel." Power Automate will watch only this folder, not the whole inbox.

---

### Phase 2 — Prepare the SharePoint destination (5 min)

1. In your SharePoint team site: **+ New → Document library** — name it **Vendor Invoices Library**
2. **+ New → List** — name it **Invoice Tracker** — with columns:
   - Title (existing)
   - From (Single line of text)
   - Received_Date (Date and time)
   - Subject (Single line of text)
   - Attachment_Count (Number)
   - Document_Link (Hyperlink)
   - Status (Choice: New / In Review / Processed / Rejected — default New)

---

### Phase 3 — Build the flow (15 min)

1. `make.powerautomate.com` → **+ Create → Automated cloud flow**
2. Name: `Test — Vendor Invoice Intake`
3. Trigger: **"When a new email arrives (V3)"** — Office 365 Outlook
4. Configure:
   - Folder: pick `Vendor Invoices`
   - Include attachments: **Yes**
   - Only with attachments: **Yes**

#### Add: List the attachments

5. The trigger already includes attachments — we'll loop through them

#### Add: Create item in Invoice Tracker

6. **+ New step → SharePoint → Create item**
7. Site: your team site; List Name: `Invoice Tracker`
8. Map fields:
   - Title: dynamic content `Subject` from email
   - From: dynamic content `From`
   - Received_Date: dynamic content `Received Time`
   - Subject: dynamic content `Subject`
   - Attachment_Count: expression `length(triggerOutputs()?['body/attachments'])`

#### Add: Loop through attachments

9. **+ New step → Control → Apply to each**
10. Output from previous: `Attachments` (dynamic content)
11. Inside the loop, add:
    - **SharePoint → Create file**
    - Site: your team site
    - Folder Path: `/Shared Documents/Vendor Invoices Library/`
    - File Name: dynamic content `Name` (from attachment)
    - File Content: dynamic content `Content Bytes` (from attachment)

#### Add: Notify Teams

12. After the loop: **+ New step → Microsoft Teams → Post message in a chat or channel**
13. Channel: pick a test channel
14. Message: 
    ```
    📬 New invoice received from @{triggerOutputs()?['body/from']}
    Subject: @{triggerOutputs()?['body/subject']}
    Attachments: @{length(triggerOutputs()?['body/attachments'])} files saved.
    Action required: review in Invoice Tracker.
    ```

#### Add: Mark original email as read

15. **+ New step → Office 365 Outlook → Mark as read or unread (V3)**
16. Message ID: dynamic content `Message Id`
17. Mark As: `Read`

18. **Save.**

---

### Phase 4 — Test (10 min)

1. Send yourself a test email with one or two PDF attachments
2. **Manually move it** to the `Vendor Invoices` folder (or wait for the rule)
3. Watch Power Automate's **Run history** — the flow should fire within 1-2 minutes
4. Verify:
   - The PDFs appear in the SharePoint library
   - A new row appears in the Invoice Tracker list
   - The Teams channel has a notification
   - The original email is marked as read

---

## 🔧 Common issues and fixes

| Issue | Fix |
|-------|-----|
| Flow doesn't trigger | Check the folder name — must match exactly (case-sensitive in some configurations) |
| Attachments don't save | Confirm the folder path in SharePoint is exact; create the library first |
| Loop fails on attachment name | Email attachments with special characters (`/`, `\`, `:`) need name sanitisation — add a Compose step to strip them |
| Teams post fails | Some tenants restrict bot posting; use a test personal account, or post to a chat instead of a channel |
| Duplicate runs | Outlook trigger sometimes fires twice; add a "Skip if already in Invoice Tracker" condition in production |

---

## 🚀 What you've unlocked

This intake flow is the **front door** for several major automation patterns:

| Add-on | What it does |
|--------|--------------|
| **AI document reading** (Module 03) | Extract invoice line items from the saved PDFs |
| **3-way match** | Compare extracted data against SAP PO and GRN |
| **OGRA disclosure intake** | Receive incident reports via email and route to compliance |
| **HSE form intake** | Capture incident forms emailed from the field |
| **Tender clarification queries** | Auto-file vendor clarification questions during open tenders |
| **CV intake for HR** | Save attachments, log applicant info to a list |

Same pattern. Different folders, different destination lists.

---

## 🚨 Production-readiness checklist

Before pointing this at a live shared mailbox:

- [ ] **Test with edge cases**: 0 attachments (should skip), 10+ attachments (should handle), large attachments (Power Automate has a 100 MB limit per file), forwarded emails (different metadata structure)
- [ ] **Add error handling**: a "Configure run after" → on failure, send yourself an alert
- [ ] **Set up a soft-fail path**: if SharePoint is unavailable, retry 3x then notify
- [ ] **Audit log**: every intake should be recorded; never overwrite existing entries
- [ ] **Kill switch**: a SharePoint flag the flow checks; if `Disabled = true`, the flow exits cleanly
- [ ] **Premium connector check**: confirm your licence supports all connectors in production

---

## ➡️ Next step

Move on to [`sharepoint_excel.md`](sharepoint_excel.md) to learn the SharePoint + Excel integration patterns.
