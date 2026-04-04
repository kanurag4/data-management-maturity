# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file static web app (`index.html`) — no build step, no dependencies to install. Open directly in a browser.

## Architecture

Everything lives in `index.html` with three embedded sections:

- **CSS** (`<style>`) — CSS custom properties for theming, scoped styles per screen
- **HTML** — Five `<div class="screen">` blocks: `screen-welcome`, `screen-industry`, `screen-questions`, `screen-challenges`, `screen-results`
- **JavaScript** (`<script>`) — All logic inline; no modules or bundler

### Key data structures

| Variable | Purpose |
|---|---|
| `INDUSTRIES` | Array of 16 industry objects `{ id, name, icon, desc }` |
| `BENCHMARKS` | Object keyed by industry id → domain scores (1–5) |
| `DOMAINS` | 7 domain definitions `{ key, label, color }` |
| `QUESTIONS` | 20 question objects `{ domain, text, options:[{level,text}] }` |
| `MATURITY_LEVELS` | 5 level definitions `{ level, name, desc, color }` |
| `answers[]` | Array of 20 integers (1–5), index-aligned with `QUESTIONS` |

### Screen flow

`screen-welcome` → `screen-industry` → `screen-questions` → `screen-challenges` → `screen-results`

Navigation is handled by `showScreen(id)`. State is held in module-level vars (`selectedIndustry`, `answers`, `currentQ`, `selectedChallenges`). `restartAssessment()` resets all state.

### Keyboard navigation (questions screen)

`1`–`5` select the answer level; `Enter` / `→` advance to next question; `←` goes back. Listener is scoped to `#screen-questions.active` only.

### Scoring

`computeScores()` averages per-domain answers → `buildResults()` renders charts + calls `saveToSheets()`.

Charts use **Chart.js** loaded from CDN (`cdn.jsdelivr.net`).

### Benchmarks

`BENCHMARKS` object maps each of the 16 industry ids → 7 domain scores (1–5). Values are derived from EDM Council DCAM community assessments, Experian Global Data Management Research, IBM Institute for Business Value surveys, and TDWI Analytics Maturity benchmarks. Update scores here when new research is available.

### PDF Export

`savePDF()` uses **html2pdf.js** (CDN). It calls `window.showSaveFilePicker()` first if the browser supports it (Chrome/Edge on HTTPS) to open a native Save As dialog; otherwise falls back to a direct browser download. Nav buttons are hidden during capture and restored via `.then()` callback.

## Recommendations

`RECO_MAP` inside `buildResults()` maps each domain key → `{ icon, title, high, med, low }`. Each advice string is 3 sentences tailored to the score band: `high` (score < 2), `med` (score 2–3.5), `low` (score > 3.5). The top 3 lowest-scoring domains are shown.

## Google Sheets Integration

Results auto-POST to a hardcoded Google Apps Script URL (`SHEETS_URL` constant near bottom of `<script>`). The Apps Script receives JSON and appends a row. To update the endpoint, change `SHEETS_URL`.

## Deployment

- Remote: `https://github.com/kanurag4/data-management-maturity`
- Branch: `main`
- No CI/CD — push to main is the release
