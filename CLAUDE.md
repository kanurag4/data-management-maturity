# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file static web app (`index.html`) — no build step, no dependencies to install. Open directly in a browser.

## Architecture

Everything lives in `index.html` with three embedded sections:

- **CSS** (`<style>`) — CSS custom properties for theming, scoped styles per screen
- **HTML** — Four `<div class="screen">` blocks: `screen-welcome`, `screen-industry`, `screen-questions`, `screen-results`
- **JavaScript** (`<script>`) — All logic inline; no modules or bundler

### Key data structures

| Variable | Purpose |
|---|---|
| `INDUSTRIES` | Array of 10 industry objects `{ id, name, icon, desc }` |
| `BENCHMARKS` | Object keyed by industry id → domain scores (1–5) |
| `DOMAINS` | 7 domain definitions `{ key, label, color }` |
| `QUESTIONS` | 20 question objects `{ domain, text, options:[{level,text}] }` |
| `MATURITY_LEVELS` | 5 level definitions `{ level, name, desc, color }` |
| `answers[]` | Array of 20 integers (1–5), index-aligned with `QUESTIONS` |

### Screen flow

`screen-welcome` → `screen-industry` → `screen-questions` → `screen-results`

Navigation is handled by `showScreen(id)`. State is held in module-level vars (`selectedIndustry`, `answers`, `currentQ`). `restartAssessment()` resets all state.

### Scoring

`computeScores()` averages per-domain answers → `buildResults()` renders charts + calls `saveToSheets()`.

Charts use **Chart.js** loaded from CDN (`cdn.jsdelivr.net`).

## Google Sheets Integration

Results auto-POST to a hardcoded Google Apps Script URL (`SHEETS_URL` constant near bottom of `<script>`). The Apps Script receives JSON and appends a row. To update the endpoint, change `SHEETS_URL`.

## Deployment

- Remote: `https://github.com/kanurag4/data-management-maturity`
- Branch: `main`
- No CI/CD — push to main is the release
