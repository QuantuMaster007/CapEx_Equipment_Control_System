# NEXUS — CapEx Equipment Control System

**FY2025 Semiconductor Equipment Operations Dashboard**

CapEx equipment program management dashboard for semiconductor manufacturing operations.

---

## Project Overview

This dashboard provides executive-level visibility into a global semiconductor equipment portfolio across capital planning, procurement, deployment, capitalization, and risk management.

Key capabilities:
- **110+ equipment records** across 10 global sites
- **Dynamic KPI calculations** that update with every filter change
- **Excel-driven dataset** — edit the spreadsheet, refresh the page, see new data
- **8 navigation pages** covering every operational domain
- **Interactive filters** for site, region, tool type, program, vendor, phase, and risk
- **Chart.js visualizations** including trajectory charts, stacked bars, doughnuts, and sensitivity analysis
- **GitHub Pages compatible** — runs entirely in the browser

---

## Architecture

```
capex-equipment-dashboard/
├── index.html              ← Single-page app shell + all 8 page templates
├── README.md
├── css/
│   └── styles.css          ← All UI styles (Playfair Display + Inter)
├── js/
│   ├── app.js              ← Master controller: boot, render, KPIs, exports
│   ├── charts.js           ← Chart.js instances and update logic
│   ├── filters.js          ← Global filter state and application
│   ├── tableRenderer.js    ← Sortable, paginated data tables
│   ├── dataLoader.js       ← SheetJS Excel parser + JSON fallback
│   └── controlTower.js     ← Risk monitoring, alerts, watchlists
├── data/
│   ├── equipment_data.xlsx ← Source of truth (edit to update dashboard)
│   └── equipment_data.json ← Fallback if Excel fetch fails
└── assets/
    └── logo.svg
```

---

## Dataset Schema

Each row in `equipment_data.xlsx` represents one piece of capital equipment.

| Column | Type | Description |
|---|---|---|
| `tool_id` | string | Unique equipment ID (e.g. EQP-100001) |
| `tool_name` | string | Display name |
| `tool_model` | string | OEM model name |
| `tool_type` | string | Equipment category (PECVD, Etch, etc.) |
| `site` | string | Manufacturing site location |
| `region` | string | Americas / APAC / EMEA |
| `oem_vendor` | string | OEM supplier name |
| `program` | string | CapEx program (NPI Alpha, etc.) |
| `phase` | string | EVT / DVT / PVT |
| `priority` | string | P1 / P2 / P3 / P4 |
| `status` | string | Current lifecycle status |
| `install_status` | string | Installation stage |
| `budget` | number | Approved budget (USD) |
| `actual` | number | Actual spend (USD) |
| `variance` | number | Actual minus budget |
| `install_date` | string | Planned/actual install date |
| `qual_date` | string | Qualification completion date |
| `ais_date` | string | AIS capitalization date |
| `utilization` | number | Equipment utilization % |
| `lead_time_weeks` | number | OEM lead time in weeks |
| `deploy_pct` | number | Deployment completion % |
| `risk` | string | Low / Medium / High |
| `asset_class` | string | Mfg Equipment / Test Equipment / etc. |
| `useful_life_yr` | number | Depreciation life in years |
| `ais_status` | string | Capitalized / Pending / In Progress |

---

## Dashboard Pages

| Page | Description |
|---|---|
| **Executive Overview** | 8 KPIs, deployment trajectory, site distribution, risk breakdown |
| **Equipment Registry** | Sortable paginated table with all tools, sub-tabs by status |
| **Early Engagement** | Buy vs reuse analysis, capital avoidance tracking |
| **Capital Forecast** | Budget vs actual, forecast accuracy trend, program/type breakdown |
| **OEM Deployment** | Vendor performance, on-time delivery, qualification rates |
| **Capitalization** | AIS tracking, asset values, depreciation schedules |
| **Demand Modeling** | Capacity vs demand curves, sensitivity scenarios |
| **Approvals + Control Tower** | Approval pipeline, risk radar, phase readiness, alerts |

---

## Local Development

No build tools required — just serve the files over HTTP:

```bash
# Python
cd capex-equipment-dashboard
python3 -m http.server 8080
# Open: http://localhost:8080

# Node.js (npx)
npx serve .
```

> **Note:** You cannot open `index.html` directly via `file://` due to browser CORS restrictions on `fetch()`. Use a local HTTP server.

---

## GitHub Pages Deployment

1. Push the project to a GitHub repository.
2. Go to **Settings → Pages → Source: Deploy from branch → `main` / `root`**.
3. Access your dashboard at `https://yourusername.github.io/capex-equipment-dashboard/`.

All fetch paths use relative `./data/equipment_data.xlsx` — no configuration needed.

---

## Updating the Dataset

1. Open `data/equipment_data.xlsx` in Excel or Google Sheets.
2. Add, edit, or delete rows. Keep column headers unchanged.
3. Save and push to GitHub.
4. Refresh the dashboard — all KPIs, charts, and tables update automatically.

---

## Technology Stack

| Library | Version | Purpose |
|---|---|---|
| SheetJS (xlsx) | Latest | Excel file parsing in-browser |
| Chart.js | 4.4.0 | All data visualizations |
| Google Fonts | — | Playfair Display + Inter typefaces |

No frameworks, no build step, no backend.

---

*CapEx Equipment Control System — FY2025 | Semiconductor Manufacturing Operations*
