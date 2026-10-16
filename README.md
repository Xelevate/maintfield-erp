# MAINTFIELD ERP — interactive HTML prototype (v1)

![Maintfield desktop ERP dashboard preview](docs/dashboard_preview.png)

A ready-to-open, **read-only demo ERP and analytics workspace** inspired by the layout of Oracle NetSuite and styled with Maintfield's green/gold corporate identity.

The sample data is **100% fictional**, generated specifically for an Egyptian company that sells/services tractors and agricultural machines. No demo customer, employee, financial or supplier record should be treated as a real Maintfield record.

## Start here

1. Open [`index.html`](index.html) in a current Chrome, Edge or Firefox browser. It is a self-contained ~605 KB file and needs no server or dependencies for demo mode.
2. Explore the home dashboard. Click a **monthly data point** to narrow the dashboard to that month, a **revenue column** to filter revenue category, or a **donut sector** to filter invoice status. The date, governorate and customer-segment selectors also cross-filter.
3. Click an area such as **Service** or **Finance** in the menu and switch between register tabs. Search, sort, page, export CSV or click a record ID to see details and linked records.
4. To connect public test data, open **Google Sheets setup → Configure all sheets**. Paste published Google Sheet CSV URLs and optional Google Form URLs, save, then click **Sync**.
5. For GitHub Pages, upload this folder to a repo and enable GitHub Pages using **Deploy from a branch → main / (root)**. The HTML demo works as static content. No JavaScript build tool is required. Add `?demo=1` to the published URL when sharing the explicit synthetic-demo mode; the dashboard always remains read-only.

## Public repository checklist

- Publish only this bundled fictional dataset. Do not add real payroll, customer, supplier, financial, contract, or employee records.
- GitHub Actions runs the dashboard smoke test on pushes and pull requests. The workflow validates the 26-table dataset, referential links, balanced demo journals, chart cross-filters, table search, record drill-down, and connector UI.
- Create a first release tag such as `v1.0.0` after the initial GitHub Pages deployment passes its smoke check.
- The public site must use only relative asset references so it works at `https://<owner>.github.io/<repository>/`.

## Included files

| Artifact | Use |
|---|---|
| `index.html` | Full offline-capable dashboard with embedded simulated records |
| `Maintfield_ERP_Data_Templates.xlsx` | Google Sheets-ready Excel workbook (26 data tabs + SHEET_INDEX) |
| `data/*.csv` | All 26 independently importable CSV tables (minimum 10 records and 5 fields each) |
| `data_manifest.json` | Table schemas, primary keys, section mappings, row counts |
| `demo_data.json` | JSON sample database for future Codex refactor |
| `docs/GOOGLE_SHEETS_SETUP.md` | CSV publishing, Forms linking and data synchronization |
| `docs/DATA_DICTIONARY.md` | Column definitions and important ID relationships |
| `docs/CODEX_IMPLEMENTATION_BRIEF.md` | Copy/paste project specification for Codex |
| `docs/SECURITY_AND_LIMITATIONS.md` | What the demo cannot safely do yet |
| `scripts/generate_demo_data.py` | Recreate consistent fictional CSV/JSON seed records |
| `scripts/build_html.py` | Embed demo records and brand mark into portable HTML |
| `scripts/build_workbook.py` | Rebuild `.xlsx` via `artifact_tool` when available |

## Sheet count by department

| Area | Sheets | Data sets |
|---|---:|---|
| CRM | 1 | customers |
| Sales | 3 | leads, quotations, sales_orders |
| Service | 6 | machines, maintenance_contracts, work_orders, service_visits, service_parts, warranty_claims |
| Inventory | 3 | products, inventory, inventory_movements |
| Procurement | 2 | suppliers, purchase_orders |
| Finance | 4 | invoices, payments, expenses, cash_transactions |
| Accounting | 2 | chart_of_accounts, journal_entries |
| HR | 2 | employees, payroll |
| Documents | 1 | documents |
| Operations | 2 | company_assets, tasks |
| **Total** | **26** | **1,958 sample records** |

You can use **one Google Spreadsheet with 26 tabs** and publish each tab as an individual CSV URL (plus the optional sheet index tab), rather than creating 26 separate spreadsheet files. Forms have their **own response tabs**; do not confuse those raw responses with the normalized ERP tabs.

## Recommended initial Google Forms (20 optional workflows)

| Area | Forms | Suggested flows |
|---|---:|---|
| CRM | 2 | New customer; lead capture |
| Sales | 2 | Quote request; order intake |
| Service | 4 | Machine registration / commissioning; work order; visit report; warranty claim |
| Inventory | 2 | Product master request; receipt / issue / stock adjustment |
| Procurement | 2 | Supplier onboarding; purchase order |
| Finance | 3 | Invoice entry; customer receipt; expense / cash payment |
| Accounting | 1 | Journal entry request and approval |
| HR | 2 | Employee records; payroll approvals (DEMO ONLY if public) |
| Documents | 1 | Document metadata intake (no sensitive uploads for public prototype) |
| Operations | 1 | Task/asset request |
| **Total** | **20** | Optional and phaseable; fewer Forms can be used at first |

Start by connecting **customers, products, machines, work_orders, invoices, payments, expenses**. Other Sheets can stay on simulated records until ready. For a coherent real report, ensure every related Sheet is from the same dataset; don't mix simulated invoices with real payments.

## Important distinctions

- **This is a working interactive HTML dashboard / reporting prototype, not a production-ready accounting ERP.** It has no authentication, user provisioning, approvals, audit logs, server-side permissions, invoice issuing, payroll calculation service, tax logic or direct write-back.
- The Excel and 26 CSVs are **editable templates**. Google Forms submissions may require a separate normalization step (including unique IDs and field names) before this app can read them.
- Data imported through public Google Sheets is **read-only** in the HTML. Clicking **Open input form** goes to the configured Google Form. Sync pulls the resulting CSV into the UI when the remote endpoint is browser-readable and supports CORS.
- Configured URLs are saved in local browser storage. Successful sync data is held only in memory and fetched again at next load. Never save a password/API key in this project.
- Dashboard revenue means invoice amounts, not bank deposits; cash receipts are shown separately. Operating expenses are company-wide even when charts are filtered by customer region; do not treat this as audited P&L.
- The independent demo journal entries balance in pairs but do **not** automatically post from invoices, stock or payments. Demo stock movement histories also do not reconcile to current stock snapshots.

## Technology

Plain HTML, CSS, native JavaScript and inline SVG charting. No hosted dependencies, tracking, external images or account credentials. Works offline in demo mode. Source data is deterministic via a Python seed generator. Brand logo was extracted from the company profile supplied for this project.

## Maintfield business grounding

The provided 2026 company profile describes a Cairo-based agricultural machinery supplier offering **Zoomlion tractors from 49 to 150 HP**, implements, **FUCHS oils**, genuine spares, preventive maintenance at **50/250/500/1000 hours**, on-farm breakdown repair, workshop jobs, PDI / commissioning, operator training, annual maintenance agreements and signed service reports tied to unique chassis numbers. The ERP structure follows those processes. The actual profile mentions **a team of 2**; the 12 sample employee rows show a fictional expanded team for HR testing only.

## Next phase

Provide Codex the entire repo plus [`docs/CODEX_IMPLEMENTATION_BRIEF.md`](docs/CODEX_IMPLEMENTATION_BRIEF.md), then ask it to create an organized GitHub repository, publish GitHub Pages and incrementally implement the backend / role security. Do **not** publish private operational Sheets while testing this public GitHub version.
