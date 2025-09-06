# NHS-AE-KPI-4hr-standard
# A&E Waiting Times — NHS England (Power BI)

**Goal**  
Track A&E performance against the 4-hour standard with trends and provider drilldowns.

**KPIs**
- **Seen Within 4 Hours %**
- **Breach Rate %** (>4 hours)
- **Total Attendances**

**Data**
- NHS England: *A&E Attendances and Emergency Admissions — Monthly CSVs (Apr–Jul 2025)*  
- Columns used: Org name, Month/Year, attendances (Type 1 & 2 & Other A&E), attendances >4hrs, emergency admissions.

**Model**
- Power Query: appended Apr–Jul; created `Month-Year` + `MonthStart`; calculated:
  - `Total Attendances = Type1 + Type2 + Other A&E`
  - `Over 4 Hours = Type1 + Type2 + Other Dept`
- DAX (key measures):
  - `Seen Within 4 Hours % = 1 - DIVIDE([Over 4 Hours], [Total Attendances])`
  - `Breach Rate % = DIVIDE([Over 4 Hours], [Total Attendances])`
  - Disconnected **Targets** table (95% / 90% / 76%) with slicer:
    - `Selected Target % = SELECTEDVALUE(Targets[Target], 0.95)`
    - `Seen % vs Selected Target (pp) = [Seen Within 4 Hours %] - [Selected Target %]`

**Pages**
1. **Overview** — KPIs, gauge vs target, trend by month, Top-10 providers by breach rate.
2. **Provider Drilldown** — Org slicer, KPI cards, columns (Total & >4h) + line (Breach %), monthly table with Δ vs target.

**Highlights (example to tailor to your run)**
- National **Seen <4h ≈ 75%** across Apr–Jul 2025 in this cut.
- Trend improves **from ~Apr to Jul** (see line chart on Page 1).
- Some providers breach at **~30–40%**; drilldown shows where Δ vs target is widest.

**How to use**
- Pick months on the slicer (Page 1).  
- On Page 2 select a provider; optionally change the target in the target slicer.

**Files**
- `/dashboard/AE-WaitingTimes.pbix`
- `/img/page1-overview.png`, `/img/page2-provider.png`
- `/data/` (sample + link to source)

