# 🛢️ Oil & Gas Fields Operations Dashboard
### المنظومة المتكاملة لمراقبة وتحليل أداء حقول وآبار النفط والغاز (North Oil Company - NOC)

A web-based dashboard and surveillance application designed for reservoir engineers, production supervisors, and petroleum operations managers.

---

## 🌟 Key Features

1. **🌐 Multi-Field Consolidated Overview & Drill-down:**
   - **All Fields Mode (نظرة عامة على جميع الحقول مجتمعة):** Aggregated metrics across all operating fields (**Khabbaz**, **Kirkuk**, **Bai Hassan**, and **Jambur**).
   - **Individual Field Detail (تفصيل كل حقل داخلها):** Click any field pill or card to inspect its reservoir formation, individual well flow rates, and choke curves.

2. **🌍 Default English Base with Instant Arabic Translation:**
   - Default interface language is **English (LTR)** using international petroleum engineering units (`STB/D`, `MMSCFD`, `WHP Psig`, `API°`).
   - One-click language switcher (`🌐 العربية`) toggles seamlessly to **Arabic (RTL)** with Cairo typography.
   - Saves language preference in `localStorage`.

3. **📊 Wells Table Direction Fixed (LTR in English, RTL in Arabic):**
   - In English: The table flows from **Left to Right**, beginning with Field and Well No. on the left and ending with API° and BS&W% on the right.
   - In Arabic: The table flips cleanly to **Right to Left**, ensuring natural readability.

4. **⚡ Interactive Visualizations (Chart.js):**
   - **Production Comparison:** Bar chart comparing Oil Rate (`STB/D`) and Gas Rate (`MMSCFD`).
   - **Production Share (%):** Doughnut chart showing contribution per field or per well.
   - **Quota Deviation (Actual vs Target):** Dynamic indicator of over/under production against NOC targets.
   - **Reservoir Diagnostics:** Wellhead pressure (WHP) decline curves across choke sizes.

5. **📊 Power BI Hub & Excel Upload:**
   - Upload any `.xlsx` or `.csv` file via browser-side `SheetJS` parser.
   - Export filtered datasets to `.csv` with UTF-8 BOM encoding.
   - Power BI integration modal with copy-pasteable **DAX measures** and live report embedding support.

---

## 📁 Repository Structure

- [`index.html`](file:///home/runner/work/build-a-landing-page-for-my/build-a-landing-page-for-my/index.html) - Main interactive application.
- [`All_Fields_Oil_Gas_Data.csv`](file:///home/runner/work/build-a-landing-page-for-my/build-a-landing-page-for-my/All_Fields_Oil_Gas_Data.csv) - Standardized dataset covering Khabbaz, Kirkuk, Bai Hassan, and Jambur fields.
- [`Khabbaz_Cleaned_Data.csv`](file:///home/runner/work/build-a-landing-page-for-my/build-a-landing-page-for-my/Khabbaz_Cleaned_Data.csv) - Original 28 natural flow test records for Khabbaz wells.
- [`POWER_BI_GUIDE.md`](file:///home/runner/work/build-a-landing-page-for-my/build-a-landing-page-for-my/POWER_BI_GUIDE.md) - Complete Power BI Desktop setup instructions and DAX formulas.
