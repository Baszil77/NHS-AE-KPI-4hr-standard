# A&E Waiting Times — NHS England (Power BI)
# NHS A&E KPI — 4-Hour Standard (Power BI)

**Goal:** Track A&E performance against the 4-hour standard with two pages:
1) **Overview** – KPIs, trend, and top providers by Breach Rate %  
2) **Provider Drilldown** – monthly columns + breach-rate line, table with Δ vs target

---

## Screenshots
<img src="img/page1-overview.png" width="1000">
<img src="img/page2-provider.png" width="1000">
<img src="img/model.png" width="800">

---

## Key Insights (Apr–Jul 2025)
- **Seen within 4 hours ≈ 75%**, **Breach Rate ≈ 25%**, **Attendances ≈ 18M** in this slice.
- **Monthly trend improving** from April → July on Seen <4h.
- **Variation by provider:** several trusts around **30–40% breach**; Δ vs **95% standard** highlights who’s furthest from target.

---

## How it’s built
- **Data**: NHS England “A&E Attendances and Emergency Admissions — Monthly CSVs” (Apr–Jul 2025).
- **Power Query**: appended monthly CSVs; created `MonthStart` (first of month) and `Month-Year`.
- **Model**:
  - `AE_Combined` (fact)
  - `Targets` (disconnected table: 95%, 90%, 76%)
  - `DimMonth` (unique MonthStart; 1:* to fact; used to sort month charts)
- **Measures**: Total Attendances, Over 4 Hours, **Breach Rate %**, **Seen Within 4 Hours %**, **Selected Target %**, **Seen % vs Selected Target (pp)**.  
  → Full list: [`/dax/measures.xlsx`](dax/measures.xlsx)

---

## Quick start
1. Open `/dashboard/AE-WaitingTimes.pbit` *(optional if provided)* **or** open your PBIX.
2. Use the **Month-Year** slicer (blanks excluded). Single-select is optional.
3. **Gauge** = Seen% vs Selected Target; **bar** = Breach Rate % by Provider; **line** = Seen% trend.

---

## Reproduce
1. Load monthly CSVs (Apr–Jul 2025) → **Append** into `AE_Combined`.  
2. Add columns:
   - `MonthStart = Date.StartOfMonth([Period])`
   - `Month-Year = FORMAT([MonthStart],"MMM yyyy")`
3. Create `DimMonth = DISTINCT('AE_Combined'[MonthStart])` with MonthNo/Year; relate **1:* to fact**.
4. Build measures (see `/dax/measures.xlsx`).  
5. Exclude **(Blank)** in Month-Year slicer.

---

## Data & License
- Data: NHS England A&E Attendances & Emergency Admissions — Monthly (Open Gov Licence v3.0).
- Code/content: MIT (see `LICENSE`).

- `/data/` (sample + link to source)

