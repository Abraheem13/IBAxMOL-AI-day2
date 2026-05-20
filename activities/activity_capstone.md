# 🏆 Capstone — End-to-End Automated Workflow

**Time required:** 45 minutes
**Format:** Groups of 3-4 from the same function
**Deliverable:** One end-to-end automated workflow diagram + working flow sketch, presented to the room

---

## 🎯 The mission

By the end of this activity, every group has designed and partially built **one end-to-end automation** combining everything from Day 2:

- **Module 01** — process map of the workflow
- **Module 02** — Power Automate flow with at least 5 steps
- **Module 03** — AI document extraction or classification step embedded

This is the proof-of-concept your group can take back to your office and pitch to your manager next week.

---

## 📋 Step 1 — Pick the right workflow (5 minutes)

The best capstone workflows have ALL these properties:

- [ ] Currently consumes 20+ hours/month across your team
- [ ] Has both a clear "intake" (email, form, document arrives) and a clear "outcome" (decision made, document filed, payment released)
- [ ] Has at least one decision point that requires human judgement (your human-in-the-loop)
- [ ] Has at least one document-reading step (where AI extracts/classifies)
- [ ] Has at least one routing or approval step
- [ ] Can be entirely contained within your team's authority (no need for IT sign-off to demonstrate)

**Examples that work well:**

| Function | Workflow |
|----------|----------|
| Procurement | Invoice intake → 3-way match → approval routing → payment release queue |
| HSE | Field form submission → severity classification → notification routing → OGRA disclosure draft |
| Maintenance | Defect report intake → work-order categorisation → permit-to-work routing → CMMS closure |
| Finance | Vendor onboarding → KYC document extraction → master data → approval → vendor portal |

---

## 📋 Step 2 — Map the swim-lane (10 minutes)

On flipchart paper, draw the swim-lane with 4-6 rows and 8-12 steps. Mark:

- 🟢 GREEN circles: steps the AI/automation does
- 🟡 YELLOW circles: human-in-the-loop checkpoints
- 🔴 RED circles: hard-stop human actions (regulator filing, payment release, contract sign)
- ⏱️ Timer icons: where the flow waits for a response

Take a photograph.

---

## 📋 Step 3 — Sketch the Power Automate flow (15 minutes)

For each green and yellow step, decide:

| Step | Power Automate trigger or action |
|------|----------------------------------|
| Document arrives by email | Outlook trigger "new email arrives" |
| Save to SharePoint | SharePoint "Create file" |
| Extract structured data | AI Builder or HTTP-to-LLM |
| Compare to PO/GRN | Two "List rows present" + Condition |
| Send for approval | Approvals "Start and wait for approval" |
| Notify Teams channel | Teams "Post message" |
| Log to audit | SharePoint "Create item" in audit list |
| Final human action | Manual SAP entry or document sign |

If you have Power Automate access, **build the first 3-4 steps** of the actual flow on your laptop. You won't finish; that's fine. Get to "trigger fires and saves to SharePoint" — that proves the concept.

---

## 📋 Step 4 — Calculate the prize (5 minutes)

For your chosen workflow:

| Metric | Current state | Future state | Saving |
|--------|---------------|--------------|--------|
| Frequency (per month) | | (same) | |
| Avg cycle time (days) | | | |
| Human hours per occurrence | | | |
| **Total team hours saved per month** | | | |
| Risk reduction (qualitative — fewer missed deadlines, fewer fraud opportunities, audit-ready trail) | | | |

This is the slide your manager cares about.

---

## 📋 Step 5 — Present (10 minutes)

Each group has 90 seconds at the front of the room:

1. **The workflow** (one sentence): what business problem does this solve?
2. **The swim-lane**: show the diagram; call out the human checkpoints
3. **The flow sketch**: show the Power Automate flow structure
4. **The savings**: hours per month, risk reduction
5. **The ask**: what would your group need from your manager to make this real? (Licence? Sandbox? Pilot dataset?)

---

## 📊 Scoring criteria

The room votes on each group's presentation:

| Criterion | Out of 10 |
|-----------|-----------|
| Real-world fit (does this solve an actual pain point we recognise?) | |
| Process map clarity (could a new joiner follow this?) | |
| Flow design (right triggers, right approvals, right audit log?) | |
| Human-in-the-loop discipline (does it respect the Automation Red List?) | |
| ROI case (numbers + risk reduction) | |

**Winning team gets** the bragging rights and a place in the alumni hall of fame at IBA CICT.

---

## 🎓 The takeaway

You came in Monday morning knowing what AI could do.

You leave Tuesday evening having **built things** with it.

The ratio of "knowing about" to "doing with" is what separates leaders from observers in the next 18 months. Day 2 is the day you became a doer.

---

## 🔄 What to do next week

1. **Pick one of the three flows you sketched** and finish building it
2. **Pilot with mock data** for 30 days; tune the prompts and routing
3. **Show your manager** the audit log after 30 days — that's the business case
4. **Scale to two more workflows** in the next quarter
5. **Become the person** your team comes to when they have an automation idea

Six months from now, you will have eliminated 200+ hours of repetitive work from your team. That's a promotion case.
