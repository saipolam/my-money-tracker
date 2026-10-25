# My Money Tracker — installable PWA

A responsive personal finance tracker with an empty first launch (no sample transactions, debts, loans, or EMI payments), local device storage, dashboard, transactions, debts, EMI loans, savings and investments (including emergency-fund goals), payment log, monthly reports, and Excel/JSON import/export. Income and expense categories are filtered by the selected transaction type.

## Files
- `index.html` — app interface and styling
- `app.js` — app logic and local persistence
- `manifest.json` — PWA install metadata
- `sw.js` — offline caching service worker
- `icon.svg` — app icon

## Run and install
PWAs need HTTPS or localhost; opening `index.html` directly from a file manager will not enable installation or service-worker offline caching.

### Quick local test on a computer
1. Put the folder on a computer with Python installed.
2. In the folder, run: `python -m http.server 8000`
3. Open `http://localhost:8000` in Chrome.
4. To test on a phone on the same Wi-Fi, use the computer's LAN IP in place of `localhost` (service workers require HTTPS for non-localhost addresses, so use a secure host for actual installation).

### Install on Android
1. Upload the entire folder to an HTTPS static host (for example, a static site host that serves folders/files) without changing the relative file paths.
2. Open the hosted URL in Chrome on Android.
3. Choose **Install app** if prompted, or Chrome menu → **Add to Home screen**.
4. Open once while online so the app shell and spreadsheet library can cache. After that, the core tracker works offline.

## Excel import/export
The app uses SheetJS from jsDelivr for `.xlsx` handling. The app itself is offline-capable, but the first visit needs an internet connection for the spreadsheet library to load and be cached. If Excel import/export is unavailable offline before the first successful online load, reconnect and reload once. JSON backup/restore is built in without that library.

Import accepts sheets named `Transactions`, `Debts`, `EMI Loans`, and `EMI Payments`, and maps the column headers from the supplied workbook. Import asks whether to replace or append records. Export creates a new workbook with the same main data sections plus summary totals and a Savings & Investments sheet.

## Privacy / storage
Records are stored in browser `localStorage` on the device. They are not automatically synced to Google Sheets or another device. Export a JSON or Excel backup before clearing browser data, uninstalling, or changing devices. This is a starter personal app, not a bank-connected financial service.

## First launch
The app starts with no transaction, debt, loan, or EMI payment records. Default category and payment-mode choices are provided, and the category dropdown changes based on whether the transaction is Income or Expense.

## Savings & investments
The Savings & investments tab lets you track current values for investment, savings and emergency-fund records, with optional target amounts and emergency-fund progress. It is a manual tracker and does not connect to banks or brokers.
