# Lead Generator SG

A B2B lead discovery tool for the Singapore market. Search for business contacts by sector, job title, target group, and location — powered by Apify's Google Maps Scraper.

## Screenshots

### Dark Mode
![Dark Mode](screenshots/app-dark.png)

### Light Mode
![Light Mode](screenshots/app-light.png)

## Features

- **Multi-criteria Search** — Filter by 17 Singapore industries, 13 B2B job titles, 5 target groups
- **Apify Integration** — Scrapes real business data from Google Maps via Apify API
- **Sortable Results Table** — Click column headers to sort, with pagination (25/page)
- **CSV Export** — Download leads as a timestamped CSV file
- **Dark/Light Theme** — Toggle between themes, preference saved to localStorage
- **Responsive Design** — Works on desktop and mobile

## Tech Stack

- HTML5 / CSS3 / Vanilla JavaScript
- [Apify API](https://apify.com) (Google Maps Scraper)
- CSS Custom Properties for theming
- No frameworks or build tools required

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/alfredang/leadgeneration.git
cd leadgeneration
```

### 2. Start a local server

```bash
npx serve
```

### 3. Open in browser

Navigate to http://localhost:3000

### 4. Enter your Apify token

When you click **Generate Leads** for the first time, you'll be prompted to enter your Apify API token. Get yours at [console.apify.com](https://console.apify.com) under **Settings > API & Integrations**.

Your token is stored in `localStorage` and never committed to the repo.

## Project Structure

```
index.html    — Main page with search form and results table
style.css     — Dark/light theme styling via CSS custom properties
data.js       — Singapore sectors, job titles, target groups
app.js        — Application logic, Apify API calls, table rendering
export.js     — CSV export utility
```

## License

MIT
