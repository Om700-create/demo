# demo

# 📊 Pinnacle Mobility 2025 - Store Readiness Dashboard

This Power BI project visualizes store setup readiness across planned locations for the year 2025, focusing on metrics like retail readiness, logistics preparedness, and operational progress. The dashboard provides a detailed overview for business teams to monitor and take action.

---

## 🗂️ Data Source

- File: `Pinnacle Mobility 2025 (Stores).xlsx`
- Sheet Used: `Pinnacle Mobility 2025 (Stores)`

---

## ✅ Key Features

- KPIs: Total Planned Stores, % Retail Ready, Pending Welcome Emails, % Printer Ready
- Charts: Status breakdown, Readiness by month
- Matrix: Per-store readiness (LMS, Decal, Phone Order)
- Slicers: Status, Email status, Month
- Optional map visualization

---

## 🧰 Tools Used

- Power BI Desktop
- DAX (Data Analysis Expressions)
- Power Query (for data cleaning)

---

## 🔁 Data Preparation Steps

1. **Import Excel Sheet**  
   - Home → Get Data → Excel → Select `Pinnacle Mobility 2025 (Stores).xlsx`

2. **Load the Sheet**:  
   - Sheet name: `Pinnacle Mobility 2025 (Stores)`

3. **Clean Columns**:  
   - Keep relevant columns: `STATUS`, `RETAIL READY DATE`, `RETAIL READY MONTH`, `WELCOME EMAIL STATUS`, `LMS`, `DECAL`, `PHONE ORDER`, `TSP ID`, `Funnel Month`
   - Remove null or irrelevant columns

4. **Standardize Values** (Power Query):
   - Replace: `"yes", "YES"` → `"YES"`
   - Replace: `"no", "NO"` → `"NO"`

5. **Close & Apply** changes

---

## 📐 Measures (DAX)

Paste these into Power BI using **Modeling → New Measure**:

```DAX
Total Stores = COUNTROWS('Pinnacle Mobility 2025 (Stores)')
DAX
Copy
Edit
Retail Ready % = 
DIVIDE(
    COUNTROWS(
        FILTER(
            'Pinnacle Mobility 2025 (Stores)',
            NOT(ISBLANK('Pinnacle Mobility 2025 (Stores)'[RETAIL READY DATE]))
        )
    ),
    [Total Stores],
    0
)
DAX
Copy
Edit
Pending Welcome Emails = 
CALCULATE(
    COUNTROWS('Pinnacle Mobility 2025 (Stores)'),
    'Pinnacle Mobility 2025 (Stores)'[WELCOME EMAIL STATUS] <> "RECEIVED"
)
DAX
Copy
Edit
Printer Ready % = 
DIVIDE(
    COUNTROWS(
        FILTER(
            'Pinnacle Mobility 2025 (Stores)',
            'Pinnacle Mobility 2025 (Stores)'[LMS] = "COMPLETED"
        )
    ),
    [Total Stores],
    0
)
🖼️ Visual Layout
🔹 Top KPIs (Card Visuals)
Total Stores

Retail Ready %

Printer Ready %

Pending Welcome Emails

🔸 Clustered Column Chart
Axis: RETAIL READY MONTH

Values: Count of TSP ID

🔸 Donut Chart
Legend: STATUS

Values: Count of TSP ID

🔸 Matrix Table
Rows: TSP ID

Columns: LMS, DECAL, PHONE ORDER

🔸 Slicers (Dropdown)
STATUS

WELCOME EMAIL STATUS

RETAIL READY MONTH

(Optional) 🌍 Map
Location: City or State

Values: Count of stores

🎨 Formatting Tips
Use consistent colors: Green = Completed, Red = Pending

Add section titles using Text boxes

Apply theme: View → Themes → Choose “Clean” or import custom

📤 Publish / Export
Option 1: Publish to Power BI Service
Save .pbix file

Go to File → Publish → Select Workspace

Option 2: Export
PDF: File → Export → PDF

PPT: File → Export → PowerPoint

📌 Notes
Ensure column names match exactly when writing DAX

Use Data View to inspect and validate column values

Use Transform Data to rename or clean inconsistent text fields

📎 License
This project is for demonstration and internal analytics purposes only. Do not distribute without company approval.

