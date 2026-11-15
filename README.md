# DX Returns Control

A returns-control dashboard for a direct-export rollout. Turn CSV exports into overdue worklists, inventory exposure metrics, snapshot comparisons, and stakeholder reports.

**[Open the live demo](https://dx-returns-control.onrender.com/)**

Explore 2,025 fictional returns directly in your browser.

## The Problem

Returns teams work across market updates, logistics partners, and spreadsheet exports. Missed deadlines, missing due dates, and high-value inventory can become difficult to track. This dashboard brings those records into an operational view.

## Who It Helps

- Operations managers monitor overdue volume, SLA status, and inventory exposure.
- Coordinators filter worklists and prepare follow-up messages.
- Leadership reviews recurring delays, snapshot changes, and stakeholder reports.

## Try It

1. Open the demo and explore the role views.
2. Upload the [baseline CSV](src/data/returns.csv) to capture the first upload snapshot.
3. Upload the [status-update example](outputs/dx-returns-upload-status-demo.csv).
4. Open Snapshots to compare the two uploads, then download a report.

Both files contain synthetic records in the full upload schema. Exported escalation worklists contain fewer columns and are intended for review.

## Synthetic Example Results

Calculated using the fixed assessment date of July 8, 2026.

| Metric | Baseline | Status-update example |
| --- | ---: | ---: |
| Total records | 2,025 | 2,025 |
| Open returns | 1,773 | 1,765 |
| Overdue returns | 1,564 | 1,558 |
| Closed returns | 252 | 260 |
| Overdue exposure | EUR 57,518,127 | EUR 57,386,627 |

These are demonstration calculations with fictional records. Real operational improvements and savings have yet to be measured. The Leadership view includes an ROI calculator with editable assumptions.

## How It Works

The browser reads and validates a selected CSV, calculates KPIs, and renders the dashboard. Each successful upload replaces the active dataset and captures aggregate metrics for an in-session comparison. Refreshing reloads the demo and loses upload history. Erase all clears the current session.

SLA classification uses explicit due dates and a five-day near-due window. Missing due dates are flagged. High-value exposure uses a top-10-percent value cutoff among open returns. Assessment dates are currently fixed for reproducible demonstrations, including uploads. Built-in demo trends are synthetic. Upload comparisons use captured metrics.

Default summaries and risk scores use deterministic rules. Optional external LLM and email integrations require server configuration and user-triggered actions.

## Data And Security

CSV processing takes place in browser memory. Selecting a file does not transmit it to the server. Optional LLM and email actions send report/evidence data through the backend to configured providers. Credentials are configured server-side.

The role selector is a demonstration control. Enterprise authentication, authorization, audit logging, and retention controls remain future work. Prompt-pattern detection provides a limited additional guardrail. See [security notes](SECURITY.md).

## Technology

Browser-native JavaScript, HTML, CSS, and Node.js, with no third-party runtime dependencies.

**Why this stack?** I chose browser-native JavaScript and Node.js as the simplest stack for a dependency-free tool that processes CSVs locally and serves optional integrations.

## Run Locally

With Node.js installed, run `npm start` and open `http://127.0.0.1:5173/`.

```sh
npm test
npm run build
```

Use `npm.cmd` on Windows where PowerShell blocks `npm.ps1`.

## Deployment And Configuration

[render.yaml](render.yaml) configures a Node web service with build command `npm run build`, start command `npm start`, and `HOST=0.0.0.0`.

Optional integrations use [.env.example](.env.example). Set `LLM_API_URL`, `LLM_API_KEY`, and `LLM_MODEL` for the LLM bridge. Set `EMAIL_WEBHOOK_URL` and, where required, `EMAIL_WEBHOOK_TOKEN` for report delivery.

The downloadable template defines the CSV schema. Export Excel workbooks as CSV before importing.
