# Data Management Maturity Assessment

A free, browser-based self-assessment tool that helps organisations evaluate their data management maturity across 7 key domains and benchmark against their industry.

## What It Does

1. **Select your industry** — 16 Australian industries covered
2. **Answer 20 questions** — across 7 data management domains (keyboard shortcuts: `1`–`5` to select, `Enter`/`→` to advance, `←` to go back)
3. **Identify your top challenges** — pick the 3 that resonate most
4. **Get your results** — radar chart, bar chart, domain scores, and tailored recommendations benchmarked against your industry
5. **Print Results** — print or save a copy of your results via the browser print dialog

## Domains Assessed

| Domain | What It Covers |
|---|---|
| Data Governance | Ownership, stewardship, policies |
| Data Quality | Accuracy, completeness, consistency |
| Data Architecture | Platforms, pipelines, storage design |
| Data Security & Privacy | Access controls, compliance, risk |
| Data Culture & Literacy | People, skills, data-driven mindset |
| Data Integration | Connectivity, interoperability |
| Analytics & BI | Reporting, insights, decision support |

## Industries Covered

Financial Services, Healthcare & Life Sciences, Retail & E-Commerce, Manufacturing, Technology, Government & Public, Energy & Utilities, Telecommunications, Education, Logistics & Transport, Mining & Resources, Agriculture & Agribusiness, Construction & Real Estate, Professional Services, Tourism & Hospitality, Not-for-Profit.

## Usage

No installation required. Open `index.html` directly in any modern browser, or visit the hosted version.

## Recommendations

Results include **Top Improvement Recommendations** for the 3 lowest-scoring domains. Each recommendation provides 3 sentences of tailored advice calibrated to your score level — foundational actions for low scores, scaling and automation guidance for mid-range, and advanced optimisation for high scores.

## Benchmark Methodology

Industry benchmarks are derived from publicly available research including:
- **EDM Council DCAM** community assessments
- **Experian Global Data Management Research** (2022–2024)
- **IBM Institute for Business Value** Data & AI surveys
- **TDWI Analytics Maturity** benchmarks

Scores represent indicative sector averages on a 1–5 scale and should be interpreted directionally.

## Tech Stack

- Single-file HTML app — no build step, no dependencies to install
- [Chart.js](https://www.chartjs.org/) (loaded from CDN) for radar and bar charts
- Google Apps Script for auto-saving results to Google Sheets

## Google Sheets Integration

Assessment results are automatically saved to a Google Sheet via Apps Script. To point to your own sheet, update the `SHEETS_URL` constant near the bottom of `index.html` with your own Apps Script deployment URL.

## Disclaimer

Results are generated based on self-reported responses and are intended for informational and exploratory purposes only. Do not use them as the sole basis for any business decisions.
