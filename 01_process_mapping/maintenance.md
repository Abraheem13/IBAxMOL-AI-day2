# 🔧 Process Mapping — Maintenance Work Order

**Time required:** 30–40 minutes
**Sample data:** [`sample_data/maintenance_workorder_flow.txt`](sample_data/maintenance_workorder_flow.txt)
**Deliverable:** SIPOC + swim-lane for work-order request → completion

---

## 🎯 What you will learn

1. Map a routine corrective maintenance job from request to closure
2. Find the **handover delays** that account for 60-80% of total cycle time
3. Identify the spare-parts and permit-to-work choke points

---

## 🧪 Exercise 1 — SIPOC

Read [`sample_data/maintenance_workorder_flow.txt`](sample_data/maintenance_workorder_flow.txt). Then build your SIPOC.

**Suggested fill:**

| Suppliers | Inputs | Process | Outputs | Customers |
|-----------|--------|---------|---------|-----------|
| Operations · Inspection · Condition monitoring | Work-order request · Defect report · Inspection finding | 1. Triage · 2. Planning · 3. Permit · 4. Parts · 5. Execution · 6. QA · 7. Close-out | Functional equipment · Updated CMMS record · Cost capture · Lessons learned | Operations · Reliability · Finance |

---

## 🧪 Exercise 2 — Swim-Lane

Rows for the maintenance process:

1. Operations / Requestor
2. Maintenance Planner
3. Maintenance Supervisor
4. Permit Issuing Authority (HSE)
5. Storeman
6. Maintenance Technician
7. QA / Reliability Engineer
8. CMMS (computerised maintenance management system)

**Friction points to mark in red:**

- 🔴 Step 3: Work-order categorisation — often languishes 2-5 days awaiting planner review
- 🔴 Step 5: Parts availability check — manual SAP lookup, often inaccurate vs actual stock
- 🔴 Step 6: Permit-to-work generation — paper forms, signature loops
- 🔴 Step 9: Spares delivery to workshop — coordination across stores, transport, workshop
- 🔴 Step 13: Post-job QA close-out — frequently delayed, distorts MTTR (mean-time-to-repair) metrics
- 🔴 Step 14: CMMS closure entry — technician often defers it until end of shift; data loss

---

## 🧪 Exercise 3 — Automation candidates

| Friction | Frequency / month | Time per occurrence | Automation candidate? |
|----------|------------------|--------------------|----------------------|
| Step 3: WO routing to planner | ~120 | 5 min | ✅ Auto-route by category |
| Step 5: Parts availability check | ~120 | 10 min | ✅ Auto-query SAP at WO creation |
| Step 6: Permit generation | ~80 | 30 min | ✅ Approval workflow with HSE digital sign-off |
| Step 9: Stores delivery coordination | ~80 | 15 min | ⚠️ Power Automate can notify, but logistics stays manual |
| Step 13: QA close-out reminder | ~80 | 5 min reminder, 30 min QA | ✅ Reminders auto; QA itself stays manual |
| Step 14: CMMS data entry | ~80 | 15 min | ⚠️ Voice/photo capture by technician; AI transcribes |

**Total addressable automation: ~95 hours/month** for a medium plant. That's half a full-time engineer recovered.

---

## 🎯 The killer use case for maintenance

**Permit-to-work workflows** combine maintenance + HSE in one approval chain. This is the single highest-value Power Automate flow most O&G operators can build. It typically eliminates:

- Lost paper forms
- Mis-signed permits
- Permits issued without spotter / standby presence verified
- Permits expiring without renewal
- Tracking gaps for tracked permits during audits

Build the permit-to-work flow first. Everything else can come later.

---

## 🤔 Common questions

**Q: Our CMMS already has workflow features. Why use Power Automate?**
A: CMMS workflows are usually rigid and require IT involvement to modify. Power Automate gives you (the user) the ability to wire flows yourself. Use both — CMMS for the system of record, Power Automate for the connective tissue.

**Q: Can we auto-create work orders from condition monitoring alerts?**
A: Yes — but with severity thresholds. Auto-create only for low-severity. High-severity should always page a human.

**Q: What about predictive maintenance — can AI predict failures?**
A: Yes (this is the Shell C3.ai case from Day 1). But predictive maintenance is **vendor-led platforms**, not Power Automate flows. Power Automate is the layer that *acts* on predictions: when the vendor system says "Pump P-103 needs attention," the flow opens the work order and assigns it.

**Q: My technicians won't update CMMS in the field — they say it's slow.**
A: This is the #1 maintenance automation win. Build a flow where the technician dictates a 30-second voice note in WhatsApp/Teams; AI transcribes and creates the CMMS entry; technician confirms by reply. Adoption goes from 40% to 90%.

---

## 🎓 What to take away

1. **Maintenance has more automation candidates per process than any other function.** Choose carefully — go for permits first.
2. **Don't replace the CMMS; connect to it.** Power Automate sits between systems and humans.
3. **Field-friendly capture** (voice, photo, WhatsApp) drives adoption. Form-heavy designs fail.

---

## ➡️ Next step

Continue with [`finance.md`](finance.md), or jump to [`../02_power_automate/`](../02_power_automate/).
