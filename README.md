# AR Cockpit

A single-screen control surface for accounts-receivable and collections operations. It turns a raw AR book into the four things a collections lead acts on every morning: where the money is aging, whether collection is slipping, who to chase first, and how much cash is realistically landing over the next quarter.

**[Live demo](https://sebastianvalenza.github.io/ar-cockpit/)** · runs instantly on synthetic data, or drop in your own AR export.

---

## The problem it solves

Collections teams answer the same question every day — *who do we chase, and in what order?* — and to answer it they open six reports: an aging report, a DSO trend, a dispute log, a promise-to-pay tracker, a cash-forecast spreadsheet and a customer drill-down. The decision is buried across all of them.

AR Cockpit collapses that reconciliation into one screen. Instead of reading aging and inferring priority, the operator sees a ranked worklist with the next action already attached to each account — the work shifts from assembling reports to making calls. Every metric carries a plain-language translation on hover, so the screen is legible to someone who doesn't live in collections while keeping the depth a finance lead expects underneath.

## What's inside

- **Aging** — the AR book split into 0–30 / 31–60 / 61–90 / 90+ buckets, with the 90+ write-off-risk figure as the headline, past-due broken out by collections desk, and the largest exposures surfaced.
- **DSO & CEI** — Days Sales Outstanding tracked against a target band over 90 days, alongside CEI (Collection Effectiveness Index), best-possible DSO and ADD (Average Days Delinquent). The chart shows *when* collection started slipping, not just that it did.
- **Worklist** — a prioritization engine that scores every account by `amount × days overdue × default risk × strategic weight` and ranks them. Disputed accounts are re-routed to "resolve dispute" rather than chased for payment, because the balance can't be collected until the dispute clears — the logic that separates a worklist from a list sorted by amount.
- **Cash Forecast** — cumulative projected collection across a switchable horizon (4w / 13w / 6m / 12m, defaulting to the 13-week treasury standard), with an optimistic / base / pessimistic band that shows real collection uncertainty instead of one falsely precise number.

## Use your own data

The cockpit ships with a deterministic synthetic book (251 B2B accounts, ~€36M, net-30/45/60) so it runs the moment it loads. The **Upload CSV** button accepts an export from any AR / O2C system — it auto-detects common column names, lets you map anything it can't match, and falls back to demo data on one click. It handles comma, semicolon and tab separators, UTF-8 (with or without BOM) and Latin-1 encodings, European or US number and date formats — so a `1.234,56` balance and a `31/12/2025` invoice date both read correctly — with a manual date-format override, and it reports any rows it has to skip rather than dropping them silently. Nothing leaves the browser.

## Part of an operations ecosystem

AR Cockpit is one of five control surfaces for a single multi-hub operation, built to follow one decision down the whole chain — *from the shift being covered to the cash being collected*. It is the last link: the cash that closes the loop the other four open.

| Stage | Tool | The question it answers |
|---|---|---|
| Capacity | [Shift Planner](https://github.com/sebastianvalenza/shift-planner) | Is the shift covered? |
| Workflow | [Ticket Triage](https://github.com/sebastianvalenza/ticket-triage) | Who takes what, without collisions? |
| Productivity | [Performance Tracker](https://github.com/sebastianvalenza/performance-tracker) | Is the team performing? |
| Retention | [Customer Cockpit](https://github.com/sebastianvalenza/customer-cockpit) | Does the base retain and grow? |
| Revenue | [Revenue Cockpit](https://github.com/sebastianvalenza/revenue-cockpit) | Are we going to make the number? |
| **Cash** | **AR Cockpit** *(this tool)* | **Did the money actually land?** |

All six run on the same four hubs (Madrid 🇪🇸 · Berlin 🇩🇪 · Warsaw 🇵🇱 · Dublin 🇮🇪), the same ten markets, the same seed and the same visual system — one company seen from six functions. The hubs are the same operating centres throughout: the deal a region books in the [Revenue Cockpit](https://github.com/sebastianvalenza/revenue-cockpit) becomes the receivable this cockpit collects, so revenue and cash are two ends of one money trail rather than two unrelated reports. Same world, different layer of the business.

## Stack

Single-file `index.html` — no backend, no build step, no framework — deployable to GitHub Pages as-is. Vanilla JavaScript for the data model and prioritization logic, Chart.js for the trend and forecast charts, PapaParse for CSV import. Synthetic data is generated from a fixed seed (`mulberry32`) so the book is identical on every load. Dark and light themes, persisted locally. Fully client-side — no credentials, no data leaving the page.

## Notes

All data is synthetic. No real customers, balances or company names appear anywhere in this repository. Account names, markets and figures are randomly generated for demonstration.

---

*[linkedin.com/in/sebastianvalenza](https://linkedin.com/in/sebastianvalenza)*
