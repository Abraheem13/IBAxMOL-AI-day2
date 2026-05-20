# 🔌 Power Automate — Connector Inventory for O&G

A quick reference to the connectors most useful for Pakistani O&G work, organised by use case.

---

## 📥 Intake / Triggers (where work begins)

| Connector | What it triggers on | Premium? | O&G use |
|-----------|---------------------|----------|---------|
| Office 365 Outlook | New email, flagged email, attachment received | No | Invoice intake, HSE form intake, customer queries |
| SharePoint | Item created/modified, file created/modified | No | Approvals, document management |
| Microsoft Forms | Form response submitted | No | Field reports, HSE forms, surveys |
| OneDrive for Business | File created/modified | No | Document workflows |
| Microsoft Teams | Message in channel, mention, button | No | Light approvals, alerts |
| Power Apps | Custom app triggers a flow | Yes (Premium) | Field data capture apps |
| Excel Online | New row added (limited) | No | Quick data triggers |
| RSS | New item in feed | No | Industry news monitoring |
| HTTP webhook | External system POSTs to a URL | Yes (Premium) | CMMS, SAP, external API triggers |

---

## ⚡ Actions (what work the flow does)

### Communications

| Connector | Action examples | Premium? |
|-----------|-----------------|----------|
| Office 365 Outlook | Send email, reply, mark read, move to folder | No |
| Teams | Post message, post in channel, get @mentions | No |
| Approvals | Start and wait for approval, create approval | No (basic) |
| Webex / Zoom | Schedule, send meeting links | Yes |

### Data and Documents

| Connector | Action examples | Premium? |
|-----------|-----------------|----------|
| SharePoint | Create item, update item, delete item, get items, create file | No |
| Excel Online (Business) | List rows, add row, update row, delete row | No |
| OneDrive | Create file, copy, move, delete | No |
| AI Builder | Extract from invoice / receipt / business card / ID; OCR; sentiment | Yes (Premium) |
| Office 365 (general) | User lookup, calendar events | No |

### O&G Adjacent (third-party)

| Connector | What it does | Premium? |
|-----------|--------------|----------|
| SAP ERP | Read tables, BAPI calls, IDoc handling | Yes (Premium, plus SAP licence) |
| Salesforce | CRM read/write | Yes (Premium) |
| ServiceNow | Tickets, CMDB | Yes (Premium) |
| Custom Connector | Anything with a REST API | Yes |

### Logic and Control

| Connector | What it does | Premium? |
|-----------|--------------|----------|
| Control | Condition, Switch, Apply to each, Do until, Scope | No |
| Data Operation | Compose, Filter array, Join, Select, Parse JSON | No |
| Variables | Initialize, Set, Increment, Decrement, Append | No |
| Date Time | Add to time, Format date, Get current time | No |
| HTTP | GET/POST/PUT/DELETE arbitrary URLs | Yes (Premium) |

---

## 🚦 Connector decision tree

**Q: Where does the work come from?**
- Email → Office 365 Outlook
- A form → Microsoft Forms
- A document upload → SharePoint or OneDrive
- A schedule → Schedule trigger
- An external system → HTTP webhook (Premium)

**Q: Where does the work go?**
- An approver → Approvals
- A team to be aware → Teams
- A list to track → SharePoint
- A spreadsheet to update → Excel Online
- A vendor / customer → Outlook (with human review!)

**Q: Do you need AI extraction?**
- One-off, low volume, anonymised → Claude/ChatGPT via copy-paste
- High volume, in-tenant, integrated → AI Builder (Premium)
- Anything in between → start with copy-paste; promote to AI Builder when ROI justifies

---

## 💸 Licensing reality check (as of 2026)

| Tier | Cost (approx) | What you get |
|------|---------------|--------------|
| Free with M365 | $0 | Basic connectors, approvals, SharePoint/Outlook/Excel/Teams |
| Power Automate Per User | ~$15/user/month | Premium connectors (HTTP, SAP, custom), Process Mining |
| Power Automate Per Flow | ~$100/flow/month | Premium connectors for shared flows used by many |
| AI Builder | ~$500/month for 1M credits | AI Builder actions inside flows |
| Dataverse | Included with Premium | Database backing for advanced workflows |

**Pakistani O&G reality:** most operators start with what's included in their existing M365 licence, then add Premium for one or two flows where ROI is clear. Don't licence widely before you've proven value.

---

## 🚨 What the licences cost vs the time you save

For one well-designed approval flow that saves 30 hours/month:

- 30 hours × ~PKR 1,500/hour for senior staff = PKR 45,000/month value
- Premium Per Flow licence: ~PKR 28,000/month
- **Net: PKR 17,000/month saving + reduced cycle time + audit trail**

The licence pays for itself after the first month if you build the right flow. Build the right flow first.
