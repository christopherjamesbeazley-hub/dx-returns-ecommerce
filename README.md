# E-commerce DX Returns

E-commerce returns dashboard for uploading CSV exports, tracking return status and refund delays, and prioritizing overdue cases across markets, sales channels, and carriers. The dashboard loads 600 synthetic returns when it opens.

## The Problem

Returns teams reconcile store and marketplace exports with warehouse and carrier updates. The dashboard highlights missed deadlines, missing due dates, and high-value returns in one worklist.

## Who It Helps

- Operations managers monitor overdue volume, SLA status, and financial exposure.
- Coordinators filter worklists and prepare follow-up messages.
- Leadership reviews recurring delays, snapshot changes, and stakeholder reports.

## Try It

1. Open the dashboard to explore the built-in e-commerce data.
2. Upload the [bundled CSV](src/data/dx-returns-ecommerce-demo-600.csv) to capture an upload snapshot.
3. Upload a second CSV using the same format and open Snapshots to compare the uploads.

The bundled file uses the 18-column upload schema. The dashboard displays the `partner` field as **Sales channel**.

## Synthetic Example Results

Calculated using the fixed assessment date of July 8, 2026.

| Metric | Demo |
| --- | ---: |
| Total records | 600 |
| Open returns | 90 |
| Overdue returns | 36 |
| Near-due returns | 27 |
| Missing due dates | 3 |
| Closed or cancelled returns | 510 |
| Overdue exposure | EUR 3,974.27 |

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
