# 🛠️ Activity — Build a Flow in 20 Minutes

**Time required:** 20 minutes
**Format:** Solo or pairs
**Purpose:** Build one working Power Automate flow today — no excuses

---

## 🎯 The mission

By the end of this activity, you have **one Power Automate flow saved and tested** in your tenant (or a sandbox tenant). The flow must:

- Have a trigger
- Have at least 3 actions
- Have run at least once successfully
- Have an audit log (even if it's just a SharePoint list with one row)

Anything beyond that is a bonus.

---

## 📋 Pick one of these starter flows

(All three are simple enough to build in 20 minutes with the walkthroughs from Module 02.)

### Starter A — "Weekly Inventory Low-Stock Alert"
- Trigger: scheduled (every Monday 08:00)
- Read: Excel inventory table from OneDrive
- Filter: rows where Quantity < Min_Level
- Send: Teams message to your test channel listing low-stock items
- Difficulty: ⭐⭐ (medium — Excel + Teams)

### Starter B — "Email-Triggered File Filer"
- Trigger: new email in `Inbox/AI_Inbox_Test` folder
- Action: extract sender + subject
- Action: save to a SharePoint list
- Action: post to a Teams channel
- Difficulty: ⭐ (easy — pure Outlook + SharePoint + Teams)

### Starter C — "Simple Approval Routing"
- Trigger: new item in SharePoint **Approval Test** list
- Action: start an approval request to yourself
- Action: on approval, update the list and email the requestor
- Action: on rejection, update the list and email the requestor
- Difficulty: ⭐⭐⭐ (slightly harder — conditional logic)

---

## 📋 The 20-minute clock

| Minute | Activity |
|--------|----------|
| 0-2 | Pick your starter; open `make.powerautomate.com` |
| 2-5 | Create the trigger; configure |
| 5-12 | Add the actions in order |
| 12-15 | Click Save; click Test (with manual trigger or test data) |
| 15-18 | Inspect the Run history; fix any failures |
| 18-20 | Capture a screenshot of the success message |

---

## 📋 Success criteria

You've succeeded if:

- [ ] Your flow shows green tick marks across all steps in Run history
- [ ] You can describe each step out loud without looking at the screen
- [ ] You spotted at least one place where the AI Builder action could later add value
- [ ] You can list two things you'd add for production (timeout, error handling, kill switch, audit log)

---

## 🚨 If you hit a wall

**"My organisation blocks Power Automate"**: Use a personal Microsoft 365 account, OR sketch the flow on paper following the walkthrough. The pattern is what matters; the tool is what implements it.

**"My connector won't authenticate"**: Common in restricted tenants. Try with a personal account; or use simpler connectors (SharePoint, OneDrive, Outlook only).

**"My flow fails on save"**: Read the error carefully. Most commonly: a field expected a string and you gave it dynamic content of the wrong type. Run history is your friend.

---

## 🎓 What this proves

In 20 minutes you went from never having used Power Automate to having a working flow saved in your tenant.

The implication is large: **most "we need IT for that" automation requests in O&G operators can actually be built by the business user in an afternoon**. The skill you need isn't programming — it's process mapping (Module 01) and discipline (Red List).

Day 2 is the day you stop waiting and start building.
