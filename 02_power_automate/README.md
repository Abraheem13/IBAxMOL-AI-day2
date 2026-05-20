# Module 02 — Power Automate Hands-On

**Why this module matters:** Power Automate is the bridge between mapping a process and actually fixing it. You will build three real flows today — not watch demos. By 17:00, you will have working automations on your own laptop.

---

## 📦 Sub-modules

| File | What you'll build |
|------|---------------------|
| [`approval_workflows.md`](approval_workflows.md) | A multi-step approval flow with conditional routing and an audit trail |
| [`outlook_triggers.md`](outlook_triggers.md) | An email trigger that auto-files attachments, extracts data, and notifies a Teams channel |
| [`sharepoint_excel.md`](sharepoint_excel.md) | A SharePoint list and Excel sheet kept in sync; daily summary auto-generated |

---

## 🧭 What Power Automate is (and isn't)

| It is | It isn't |
|-------|----------|
| A low-code workflow tool for office work | A replacement for SAP, CMMS, ERP |
| A connector between Microsoft + 1,000+ third-party services | A heavy data-processing engine |
| Configurable by business users (with practice) | Free of governance — IT still owns the tenant |
| Strong on approvals, email, file actions, notifications | Strong on heavy-volume real-time transactions |
| Great for "office productivity" automation | Great for SCADA / DCS / control-system work |

---

## ⚠️ Setup — what you need

| Item | Detail |
|------|--------|
| Microsoft 365 account | Work account if your org has Power Automate enabled; personal Microsoft account otherwise |
| Power Automate access | Go to `make.powerautomate.com` — sign in |
| Premium connectors | Some features require a Premium licence; we'll flag these as "Premium" in each lab |
| Practice tenant | If your work tenant blocks Power Automate, sign up for a [Microsoft 365 Developer Programme](https://developer.microsoft.com/microsoft-365/dev-program) free sandbox |

If none of the above is available, you can still:
- Watch the instructor's screen-recorded build
- Read every walkthrough end-to-end
- Sketch your flow on paper using the same logic
- Apply the patterns to whatever automation tool your IT has provisioned (Zapier, n8n, custom RPA)

---

## ✅ Pre-flight checklist

- [ ] You can sign in to `make.powerautomate.com`
- [ ] You have a SharePoint list **OR** an Excel file in OneDrive that you can write to
- [ ] You have an Outlook mailbox you can send test emails from / to
- [ ] You have read [`resources/automation_red_list.md`](../resources/automation_red_list.md)
- [ ] You have **a test recipient** ready (your own email, not anyone external)

---

## 🎓 Learning outcomes

By the end of this module you will:

1. Build an approval flow with conditional logic and a clear audit log
2. Trigger automations from incoming Outlook email and route attachments
3. Read/write SharePoint lists and Excel files, and generate scheduled summaries
4. Diagnose a failed flow run using the **Run history** tab
5. Apply the kill-switch and test-mode discipline from the Automation Red List

---

## 🧪 The single most important habit

**Every flow starts with the trigger pointed at a test mailbox or test list. Never live data on the first run.**

This is the equivalent of leak-testing before you open the main valve. Same engineering discipline; different domain.
