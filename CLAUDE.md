# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Lead Generator SG is a B2B lead discovery tool for the Singapore market. It's a frontend-only single-page application (vanilla HTML/CSS/JS, no framework, no build step) that integrates with the Apify API to scrape Google Places data.

## Running the App

```bash
npx serve        # Serve on localhost:3000
```

No build, lint, or test commands — open `index.html` via any static server.

## Architecture

```
index.html   — Page structure: search form, results table, state containers
data.js      — Constants: SECTORS (17), JOB_TITLES (13), TARGET_GROUPS (5)
app.js       — All application logic (IIFE, no modules)
export.js    — CSV export utility (exportToCSV)
style.css    — Dark/light theming via CSS custom properties + data-theme attribute
.mcp.json    — Apify + Playwright MCP server configs
```

Scripts load in order: `data.js` → `export.js` → `app.js`. All share the global scope.

## Data Flow

1. User selects sectors, job titles, target group, location, keywords
2. `buildSearchQueries()` constructs up to 5 search strings
3. `runApifyActor()` calls Apify's synchronous endpoint (`run-sync-get-dataset-items`) using the `compass~crawler-google-places` actor
4. `parseApifyResults()` normalizes response into lead objects
5. `renderTable()` displays leads with sorting and pagination (25/page)
6. `exportToCSV()` downloads results as CSV

## Key Patterns

- **State management**: `showState(state)` toggles visibility between `empty`, `loading`, `error`, `results`
- **Theming**: `data-theme` attribute on `<html>`, CSS custom properties (--bg, --text, --accent, etc.), persisted to localStorage
- **Multi-select dropdowns**: Custom-built with checkboxes, no library
- **XSS protection**: `esc()` function for HTML escaping in table rendering
- **Apify token**: Hardcoded in app.js (frontend-exposed)

## Lead Object Schema

Fields: `companyName`, `industry`, `contactPerson`, `jobTitle`, `email`, `phone`, `website`, `linkedin`, `companySize`, `location`, `source`, `dateFound`. Contact person, job title, LinkedIn, and company size are always "N/A" (not available from Google Places).
