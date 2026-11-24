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

- **Topline metrics** — Membership, ASA, pledge units, average pledge, operating revenue, expenses, outreach, and **mission field reach** (membership ÷ population), each shown against the trailing **3-year average**.
- **Trend over time** — Choose any metric (defaults to ASA), including **Mission Field Reach %** (membership ÷ population) to compare how far congregations reach into their local mission fields. The chart automatically switches to a *by-church* view when any filter is active, and otherwise shows the diocesan aggregate. This selector also drives the convocation and region breakdown charts.
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
- **Stewardship** now overlays the **diocese-wide average pledge** (weighted, per year) for context against each church's own average pledge.
- **Mission field reach.** A radius dropdown (1, 2.5, 5, 10 or 20 miles; default 5) drives a Mission Field Reach KPI (membership ÷ population within the radius), a chart of population, membership and reach over time, and a list of the other Episcopal churches within the same radius, nearest first, each linking to its own page.
- Full annual data table with CSV export.

## Data

- **Coverage:** 160 congregations, reporting years **2000–2025**.
- **Dimensions:** 3 church types (Mission, Parish, Special Evangelical Mission), 4 regions (East, North, South, West), 11 convocations.
- **Metrics (21):** membership, communicants, ASA, Easter/Christmas attendance, marriages, burials, baptisms, confirmations, receptions, pledged amount, pledge units, average pledge, plate & pledge, operating/non-operating/total revenue, expenses, outreach, diocesan assessment, and capital funds.

All data is embedded directly inside `index.html` as a JavaScript object, alongside Texas county boundary geometry for the map. There is no external database or API call — the page is fully portable.

**Mission field population.** Each church carries an estimated population within 1, 2.5, 5, 10 and 20 miles of its street address, **per year (2000–2025)**. Every populated 2020 U.S. Census block in Texas (2020 Redistricting Data, PL 94-171) counts if its center point falls within the radius. Each block is scaled to each year by its own county's growth, using Census Bureau annual county population estimates (intercensal 2000–2009, Vintage 2020 for 2010–2019, Vintage 2025 for 2020–2025). Only Texas population is counted. Figures are estimates, not exact counts.

**Diocese-wide reach.** The main page's Mission Field Reach % is total membership ÷ the population of the diocese, so each person is counted once. From 2022, when the North Region (formerly the Episcopal Diocese of Fort Worth) joined, that is 81 counties: the 57 historic Diocese of Texas counties, 23 whole North Region counties, and the part of Grand Prairie that lies in Dallas County. For 2000–2021 it is the 57 historic counties, since the source data has no North Region churches before 2022. The drop between 2021 and 2022 reflects that boundary change. Populations are Census Bureau annual county estimates, plus the Census estimate for Grand Prairie's Dallas County part. When filters are applied, the number is the filtered churches' members ÷ the same diocesan population.

**Church locations.** Each church is placed at its physical street address (latitude and longitude stored with the church). About 30% of addresses in the source data are mailing P.O. boxes, so physical addresses were confirmed from each church's website and the diocesan directory, and a few were pinned by hand. The nearby church list is calculated in the page from these locations.

## Technical notes

- **Single file:** Everything (HTML, CSS, JavaScript, data, and map geometry) lives in `index.html`.
- **Charting:** [Chart.js 4.4.1](https://www.chartjs.org/) is loaded from a CDN, so an internet connection is required for charts to render. The page itself works offline; only the chart library is remote.
- **No build step:** Plain HTML/CSS/JS — open it, host it, or commit it as-is.
- **Browser support:** Any current version of Chrome, Edge, Safari, or Firefox.
- **Mobile:** Both the main dashboard and individual church pages are responsive and optimized for phone-sized screens.

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
