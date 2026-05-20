# 🗂️ Power Automate — SharePoint & Excel Integration

**Time required:** 30–40 minutes
**You will build:** Keep a SharePoint list and an Excel sheet in sync; generate a daily Teams summary

---

## 🎯 What you will build

Three reusable patterns:

1. **Two-way sync** between a SharePoint list and an Excel table (changes in either reflect in the other)
2. **Daily scheduled summary** that reads Excel data and posts a digest to Teams every morning at 08:00
3. **Manual-trigger button** that exports a filtered SharePoint view to a formatted Excel file on demand

---

## 🧭 Setup (5 min)

1. Open your Invoice Tracker SharePoint list from the previous lab (or create a fresh **Inventory Tracker** list with: Item, Quantity, Min_Level, Location, Last_Updated)
2. Create an Excel file in OneDrive — `inventory_summary.xlsx`
3. Inside the Excel, create a Table (highlight a few rows + headers → Insert → Table → check "My table has headers")
4. Name the Table `tbl_Inventory` (formula bar → Table Design tab → rename)

> Power Automate **only sees Excel Tables**, not free-form spreadsheets. This is the most common stumbling block — convert your range to a table first.

---

## 🧪 Pattern 1 — SharePoint → Excel sync (15 min)

### Build flow A: when SharePoint item is added or modified, add/update Excel row

1. `make.powerautomate.com` → **+ Create → Automated cloud flow**
2. Name: `Test — SharePoint to Excel sync`
3. Trigger: **"When an item is created or modified"** (SharePoint)
4. Configure: Site + List = your Inventory Tracker list

#### Check if the item already exists in Excel

5. **+ New step → Excel Online (Business) → List rows present in a table**
6. Location: OneDrive
7. File: `inventory_summary.xlsx`
8. Table: `tbl_Inventory`
9. Filter Query: `Title eq '@{triggerOutputs()?['body/Title']}'`

#### Condition: does it exist?

10. **+ New step → Control → Condition**
11. Condition: `length(outputs('List_rows_present_in_a_table')?['body/value'])` is greater than `0`

#### Yes branch (already exists — update)

12. **Excel Online → Update a row**
13. Key Column: Title; Key Value: matches the SharePoint Title
14. Map the rest of the columns to SharePoint dynamic content

#### No branch (doesn't exist — add)

15. **Excel Online → Add a row into a table**
16. Map all columns

17. **Save and test.** Add a row to the SharePoint list. Watch Excel update within a minute.

---

## 🧪 Pattern 2 — Daily summary to Teams (10 min)

### Build flow B: scheduled at 08:00, summarises low-stock items, posts to Teams

1. **+ Create → Scheduled cloud flow**
2. Name: `Daily inventory low-stock alert`
3. Recurrence: every 1 day at 08:00

#### Read all rows from Excel

4. **Excel Online → List rows present in a table** → `tbl_Inventory`

#### Filter for low stock

5. **+ New step → Data Operation → Filter array**
6. From: dynamic content `value` (from previous step)
7. Condition: item `Quantity` is less than item `Min_Level`

#### Build the message

8. **+ New step → Data Operation → Compose**
9. Inputs: a markdown summary like:
   ```
   🔔 Daily Inventory Alert — @{utcNow('dd MMM yyyy')}
   
   Items below minimum stock level: @{length(body('Filter_array'))}
   
   Details:
   @{join(xpath(xml(json(concat('{"root":', body('Filter_array'), '}'))), '//Item/text()'), ', ')}
   ```
   
   (Or use a simpler approach: loop through the filtered array and append to a string variable.)

#### Post to Teams

10. **+ New step → Microsoft Teams → Post message in a chat or channel**
11. Channel: your operations channel
12. Message: dynamic content from the Compose

13. **Save and test.** Manually trigger it from the Power Automate UI; verify the Teams post appears.

---

## 🧪 Pattern 3 — On-demand export button (10 min)

### Build flow C: button-triggered export of SharePoint data to a fresh Excel file

1. **+ Create → Instant cloud flow**
2. Name: `Export inventory snapshot`
3. Trigger: **"Manually trigger a flow"**

#### Read all items from SharePoint

4. **SharePoint → Get items**
5. Site + List = Inventory Tracker

#### Create a new Excel file in OneDrive

6. **OneDrive → Create file**
7. Folder Path: `/Inventory Snapshots/`
8. File Name: `inventory_@{utcNow('yyyy-MM-dd_HH-mm')}.xlsx`
9. File Content: start with an empty Excel template (you can upload a template Excel and reference its content here, or use the Office Scripts API for a fully formatted output)

#### Add rows from SharePoint into the new Excel

10. **+ Apply to each** → output from "Get items"
11. Inside: **Excel Online → Add a row into a table** → using the newly created file and your template's table name

12. **Save.** Run the button. A snapshot Excel appears in `/Inventory Snapshots/` with the current state.

---

## 🔧 Troubleshooting

| Issue | Fix |
|-------|-----|
| "Table not found" | Excel must contain a named Table; can't be a plain range |
| Excel updates seen with a delay | OneDrive sync can take 30-60s; not a flow bug |
| Filter array always empty | Check the comparison data types (string vs number; Excel often stores as text) |
| Two flows fighting (Excel → SP and SP → Excel) | Add an "updated by" filter; or run only one direction |
| Scheduled flow doesn't fire | Check the time zone in the recurrence settings — defaults can be UTC, not PKT |

---

## 🎓 Why these patterns matter

| Pattern | Real-world use |
|---------|----------------|
| SharePoint ↔ Excel sync | Make data accessible to both technical (SP) and non-technical (Excel) users |
| Daily Teams summary | Replace 15 manual emails with 1 automated post; surface what matters |
| On-demand export | Audit pulls, ad-hoc reports, weekly board pack — no more manual SAP export |

These three combined cover **80% of office-automation requests** in a typical O&G operator.

---

## 🚨 Production-readiness reminders

- Excel files in OneDrive have a **5 MB / 1 million-row** ceiling for Power Automate reads. Above that, use SQL or Dataverse.
- Multiple flows writing to the same Excel can collide. Use SharePoint Lists as the system of record where possible.
- Scheduled flows can fail silently if your Power Automate licence is downgraded. Set up failure alerts on the flow owner.
- For high-volume needs (>1,000 transactions/day), Power Automate isn't the right tool — escalate to your IT team for proper integration.

---

## ➡️ Next step

Move on to **Module 03 — AI Document Reading** in [`../03_ai_document_reading/`](../03_ai_document_reading/). The flows you built here will become the **acting layer** for documents the AI processes.
