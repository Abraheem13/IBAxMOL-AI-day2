# 📖 Glossary — Day 2 Terms

Day 2 introduces several terms from process discovery, RPA, and Power Automate. This is a quick reference; see also the Day 1 glossary for AI-specific terms.

---

## A

**AI Builder** — A premium add-on to Power Automate that brings pre-trained AI models (invoice extraction, receipt extraction, OCR, sentiment) into flows. Costs ~$500/month for 1M credits.

**Approvals** — A Power Automate action that pauses a flow until a named human responds with approve/reject. The single most important action for human-in-the-loop automation.

**Audit log** — A record of every automated decision: timestamp, input, output, who/what approved, confidence score. Non-negotiable for compliance-relevant flows.

---

## C

**CAPA** — Corrective and Preventive Actions. An action set generated from incident or audit findings; each has an owner, target date and verification method.

**CMMS** — Computerised Maintenance Management System. The system of record for maintenance (asset masters, work orders, planned maintenance, spare parts). Common in O&G: SAP PM, Maximo, eMaint.

**Connector** — Power Automate's term for an integration with another service (SharePoint, Excel, SAP, Salesforce). 1,000+ connectors available. Some are free, some Premium.

---

## D

**Dataverse** — Microsoft's database service underlying Power Platform. Use for advanced workflows; not needed for basic flows.

**Document AI** — Catch-all for AI that reads unstructured documents (PDFs, scans, photos) and outputs structured data.

---

## F

**Flow** — A single Power Automate workflow. Made up of one trigger + one or more actions.

**Friction point** — A step in a process where work waits, gets re-done, or is manually re-entered. Friction points are automation candidates.

---

## G

**GRN** — Goods Receipt Note. The document confirming goods have been delivered against a PO. The middle of the "3-way match" (PO + GRN + Invoice).

---

## H

**Human-in-the-loop (HITL)** — The discipline of inserting a named human checkpoint before any consequential or irreversible action in an automated workflow. Always required for: payments, regulatory filings, external communications, deletions.

---

## I

**Intake layer** — The collection of triggers and pre-processing that capture incoming work (emails, forms, documents) and prepare it for downstream automation.

---

## K

**Kill switch** — A control (typically a SharePoint flag or named admin email) that stops a flow without deleting it. Required on any production flow.

**KYC** — Know Your Customer. The verification process for new vendors or counterparties.

---

## M

**MTTR** — Mean Time To Repair. A maintenance metric. Often distorted by delayed CMMS closure — fix that, and your MTTR improves without doing any real work differently.

---

## O

**OCR** — Optical Character Recognition. Reading text from images (scanned PDFs, photos of paper forms).

---

## P

**Power Automate** — Microsoft's low-code workflow tool. Lives at `make.powerautomate.com`. Used for office automation (approvals, email handling, document workflows) — not for high-volume transaction processing.

**Power Apps** — Microsoft's low-code app builder. Can trigger Power Automate flows from custom-built forms / mobile apps.

**Power Platform** — Umbrella for Power Automate, Power Apps, Power BI, Power Pages, Power Virtual Agents.

**PPRA** — Public Procurement Regulatory Authority of Pakistan. Sets rules for public procurement. PPRA Rule 36 covers justifications for non-open methods.

**Premium connector** — A connector that requires a paid Power Automate licence (HTTP, SAP, custom APIs, AI Builder). The free tier connectors are sufficient for most basic flows.

**PTW / Permit-to-Work** — A document authorising specific work in specific conditions (hot work, confined space, height, electrical isolation). High-friction process; perfect Power Automate use case.

---

## R

**RPA** — Robotic Process Automation. Software bots that mimic human actions in user interfaces (clicking buttons, copying fields between systems). Distinct from Power Automate, which is API-driven. UI-Path, Automation Anywhere, Blue Prism are RPA tools. Power Automate has limited RPA features.

**Reversibility** — The ease of undoing an action. Sending an internal reminder = highly reversible. Releasing a payment = irreversible. The Automation Red List uses reversibility as the primary filter.

---

## S

**SAP** — System, Applications and Products — the dominant enterprise ERP. Common in Pakistani O&G operators. Power Automate connects via Premium SAP connectors, requires SAP licence too.

**SIPOC** — Suppliers, Inputs, Process, Outputs, Customers. The 30,000-ft view of a process. First step in mapping; second step is swim-lane.

**Swivel-chair work** — Manual copying of data from System A into System B because the systems don't talk to each other. Classic automation candidate.

**Swim-lane** — Process diagram with rows (roles/systems) and columns (time). Shows handoffs clearly. The diagram developers need before building a flow.

---

## T

**Trigger** — The event that starts a Power Automate flow (new email, scheduled time, item created, button pressed).

**Three-way match** — Comparing Purchase Order + Goods Receipt Note + Invoice to confirm payment is justified. The killer use case for AI document reading in finance.

---

## W

**WHT** — Withholding Tax. Tax deducted at source from vendor payments per FBR (Federal Board of Revenue) rates. Determined by vendor category.

**Work order (WO)** — A formal request to do maintenance work on a specific asset. Created in the CMMS.
