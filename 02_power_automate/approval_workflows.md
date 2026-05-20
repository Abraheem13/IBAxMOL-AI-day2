# 📋 Power Automate — Approval Workflows

**Time required:** 40–50 minutes
**You will build:** A real working approval flow for a small purchase request

---

## 🎯 What you will build

A flow that:
1. Triggers when an item is added to a SharePoint "Purchase Requests" list
2. Routes to **Manager** for first approval (any amount)
3. **Conditional routing**: if amount > 50,000 PKR, also routes to **Finance Manager**
4. On approval: notifies requestor, posts to a Teams channel, logs to an audit list
5. On rejection: notifies requestor with rejection reason, logs the rejection

This is the canonical Power Automate "first build." It's directly useful for procurement, finance, HSE permits, and IT requests.

---

## 🧭 Step-by-step build

### Phase 1 — Set up the SharePoint list (5 min)

1. Go to `sharepoint.com` → your team site (or any team site you can edit)
2. **New → List** → "Blank list" → name it **Purchase Requests Test**
3. Add these columns:
   - `Title` (already exists) — short description of what's being purchased
   - `Amount_PKR` (Currency)
   - `Justification` (Multiple lines of text)
   - `Requestor_Email` (Single line of text)
   - `Status` (Choice: Pending / Approved / Rejected — default Pending)

> **Anonymisation reminder:** use mock data only. No real vendor names, no real amounts.

---

### Phase 2 — Create the approval flow (15 min)

1. Go to `make.powerautomate.com`
2. **+ Create → Automated cloud flow**
3. Name: `Test — Purchase Request Approval`
4. Trigger: **"When an item is created"** (SharePoint connector)
5. Configure: Site Address = your team site; List Name = Purchase Requests Test

#### Add a Manager Approval step

6. **+ New step → Approvals → Start and wait for an approval**
7. Approval type: **Approve / Reject — First to respond**
8. Title: `Purchase Request: @{triggerOutputs()?['body/Title']}`
9. Assigned to: your own email for testing (later, this becomes the Manager's email)
10. Details: include amount, justification, requestor (use the dynamic content picker)

#### Add Condition for high-value requests

11. **+ New step → Control → Condition**
12. Condition: `Amount_PKR` is greater than `50000`

#### Inside the "Yes" branch:

13. **+ Add an action → Approvals → Start and wait for an approval**
14. Title: `Finance Manager Approval: @{triggerOutputs()?['body/Title']}`
15. Assigned to: your test email (later: Finance Manager)

#### After the condition (regardless of branch):

16. **+ New step → Control → Condition** — check if approval response = Approve
17. **Yes branch:**
    - SharePoint → Update item — set `Status` to `Approved`
    - Office 365 Outlook → Send email — to requestor with approval confirmation
    - Microsoft Teams → Post message in a chat or channel — to your team's approvals channel
    - SharePoint → Create item — in an audit list (or append a row to an Excel audit log)
18. **No branch:**
    - SharePoint → Update item — set `Status` to `Rejected`
    - Office 365 Outlook → Send email — to requestor with rejection reason
    - SharePoint → Create item — audit log entry

19. **Save.** Yes, that's the whole flow.

---

### Phase 3 — Test it (10 min)

1. Go back to your SharePoint list
2. Click **+ New** — add a test purchase request:
   - Title: `Test stationery order`
   - Amount: `10000`
   - Justification: `Quarterly office stationery for OGTI test`
   - Requestor email: your own email
3. **Check your email or the Power Automate mobile app** — you should have an approval request waiting
4. Approve it
5. Watch the rest of the flow execute — you should receive confirmation, the SharePoint Status should update, the Teams channel should have a post, and the audit log should have a new row

If anything fails: Power Automate's **Run history** tab tells you exactly which step failed and why.

---

### Phase 4 — Test the high-value branch (5 min)

1. Create a second item with `Amount_PKR = 75000`
2. You should now receive **two** approval requests (Manager + Finance Manager)
3. Approve both
4. Verify the audit log captures both approvals

---

## 🔧 Common issues and fixes

| Issue | Fix |
|-------|-----|
| "Connection not found" error | Power Automate prompts you to sign in to each connector once; re-authenticate |
| Approval email never arrives | Check spam; also verify the "Assigned to" field is your correct email |
| Teams post fails | Premium connector may be required; or your tenant blocks the Teams API for your account |
| SharePoint update fails | Confirm the Status column has the exact choices "Pending", "Approved", "Rejected" |
| Multiple approvals required but only one fires | Switch from "First to respond" to "Everyone must approve" |

---

## 🎓 What you just learned

You can now build:

- **Permit-to-Work approval flows** (HSE + Maintenance + Operations chain)
- **Leave-request flows** (HR)
- **Vendor onboarding** (Procurement + Finance + Legal)
- **CAPA action sign-off** (HSE)
- **Spending threshold approvals** (Finance) — directly applicable to PPRA-compliant routing

The pattern is the same. Only the columns and routing logic change.

---

## 🚨 Before you deploy this in production

- [ ] Replace test emails with actual approver emails
- [ ] Add a **timeout** on each approval step (typically 5-7 days), with auto-escalation
- [ ] Verify the audit log captures: requestor, amount, approvers, timestamps, decision, comments
- [ ] Set up failure-notification alerts so you (the flow owner) get emailed if the flow breaks
- [ ] Add a kill-switch (a way to turn off the flow without deleting it)
- [ ] Pilot with one department for 30 days before scaling

---

## ➡️ Next step

Move on to [`outlook_triggers.md`](outlook_triggers.md) to learn Outlook-triggered automations.
