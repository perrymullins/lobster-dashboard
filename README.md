# EDOT Congregational Data Dashboard

An interactive dashboard for exploring congregational data from across the Episcopal Diocese of Texas. It lets diocesan staff browse trends, compare congregations, view geographic distribution, and drill into individual church profiles — all in a single, self-contained web page.

## Live site

The dashboard is published from `index.html`. If GitHub Pages is enabled for this repository (Settings → Pages → Deploy from branch → `main` / root), it will be available at:

```
https://<your-username>.github.io/lobster-dashboard/
```

You can also open `index.html` directly in any modern browser — no server or build step required.

## Features

**Main dashboard**

- **Topline metrics** — Membership, ASA, pledge units, average pledge, operating revenue, expenses, and outreach, each shown against the trailing **3-year average**.
- **Trend over time** — Choose any metric (defaults to ASA). The chart automatically switches to a *by-church* view when any filter is active, and otherwise shows the diocesan aggregate. This selector also drives the convocation and region breakdown charts.
- **Geographic distribution** — A county choropleth map zoomed to the diocesan footprint, shadable by church count, membership, ASA, operating revenue, outreach, or pledge units.
- **Size tier mix** — Congregations grouped by the diocesan "One Size Does Not Fit All" ASA tiers (Family ≤75, Pastoral ≤150, Transitional ≤225, Program ≤450, Resource >450).
- **By convocation / by region** — Bar breakdowns of the selected trend metric.
- **Scale & resources** — A bubble chart of ASA vs. operating revenue, sized by pledge units and colored by tier.
- **Church detail table** — Sortable, searchable table of all congregations with a one-click CSV export.

**Filtering**

- Filter by reporting year, church type, region, convocation, and size tier.
- Select specific churches to compare them directly.
- A reset button restores all filters.

**Header church search**

- A "Jump to a church" search box in the header opens any congregation's detail page from anywhere, including from one church page to another — no need to return to the main dashboard first.

**Individual church pages**

- Header KPIs with year-over-year deltas.
- Membership & attendance, attendance patterns (Sunday vs. Easter & Christmas), operating finances (revenue, expenses, plate & pledge, outreach), stewardship (pledge units & average pledge), outreach intensity, sacramental life, and an ASA size-tier journey chart.
- Full annual data table with CSV export.

## Data

- **Coverage:** 160 congregations, reporting years **2000–2025**.
- **Dimensions:** 3 church types (Mission, Parish, Special Evangelical Mission), 4 regions (East, North, South, West), 11 convocations.
- **Metrics (21):** membership, communicants, ASA, Easter/Christmas attendance, marriages, burials, baptisms, confirmations, receptions, pledged amount, pledge units, average pledge, plate & pledge, operating/non-operating/total revenue, expenses, outreach, diocesan assessment, and capital funds.

All data is embedded directly inside `index.html` as a JavaScript object, alongside Texas county boundary geometry for the map. There is no external database or API call — the page is fully portable.

## Technical notes

- **Single file:** Everything (HTML, CSS, JavaScript, data, and map geometry) lives in `index.html`.
- **Charting:** [Chart.js 4.4.1](https://www.chartjs.org/) is loaded from a CDN, so an internet connection is required for charts to render. The page itself works offline; only the chart library is remote.
- **No build step:** Plain HTML/CSS/JS — open it, host it, or commit it as-is.
- **Browser support:** Any current version of Chrome, Edge, Safari, or Firefox.

## Repository structure

```
index.html              # The dashboard (main file going forward)
README.md               # This file
```

The previous build (`EDOT-Dashboard.html`) is retained in an `archive/` folder in the working directory and is not part of the published site.

## Updating the data

The dashboard reads from the `DATA` object embedded near the top of `index.html`. To refresh with a new year of reporting:

1. Update the `DATA` object — add the new year to `DATA.years` and append the corresponding row to each church's `rows` array (rows follow the order defined in `DATA.keys`).
2. Save and re-upload `index.html`.

Because the data is inline, no separate data file or pipeline needs to be deployed.

## Credits

Built for the Episcopal Diocese of Texas. Size tiers follow the diocesan "One Size Does Not Fit All" framework based on Average Sunday Attendance.
