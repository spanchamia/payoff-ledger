# Payoff Ledger

A small web app for paying off a loan faster. Track a car loan, mortgage, student loan or any fixed-rate installment loan, log the extra principal payments you make, and see exactly how much interest they have erased and how much sooner you'll be debt-free.

It's a single static page with no build step and no server. It installs to your phone's home screen and works offline.

## Features

- **Burn-down view**: balance today, percent paid off, projected payoff date, and a chart of your path against the original schedule.
- **Extra payment log**: record each extra principal payment by date. It's applied with that month's scheduled payment and the whole schedule is recalculated.
- **Savings**: lifetime interest erased by your extra payments, months shaved off, and interest avoided so far.
- **Guaranteed return (APY)**: an extra dollar of principal earns exactly the loan's rate, so the app shows it as an APY you can compare with savings accounts or bonds.
- **What-if slider**: try a monthly extra amount, see the new payoff date and savings, and save it as your plan.
- **Full payment schedule** with past, current and future months.
- **Multiple loans**, plus backup and restore to a JSON file.

## Run it

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8000
```

The service worker (offline support) only runs over `http://localhost` or HTTPS.

## Host on GitHub Pages

1. In the repo, go to **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, then **Save**.
3. After a minute the app is live at `https://<your-username>.github.io/payoff-ledger/`.

## Add to your home screen

- **iPhone (Safari)**: open the site, tap **Share**, then **Add to Home Screen**.
- **Android (Chrome)**: open the site, tap the **⋮** menu, then **Install app** or **Add to Home screen**.

## Your data

Loans are stored in your browser's local storage on that device only. Nothing is sent anywhere. Use **Download backup** now and then, and **Restore from backup** to move to a new device. Clearing site data in your browser deletes your loans.

## How the math works

- Monthly payment: standard amortization, `P · r / (1 − (1 + r)^−n)` with `r = APR / 12`, rounded to the cent. You can enter your lender's exact figure instead.
- Interest is charged monthly on the remaining balance and rounded to the cent; the final scheduled payment absorbs the rounding difference.
- An extra payment is applied with the latest scheduled payment due on or before its date.
- "Interest erased" = total interest on the original schedule − total interest with your logged extra payments.
- APY = `(1 + APR/12)^12 − 1`. If you deduct mortgage interest on your taxes, your effective return is somewhat lower.

Results are estimates and can differ from your lender's statement by a few dollars (for example, if your lender charges daily interest).

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: markup, styles and script |
| `manifest.webmanifest` | Name, colors and icons for installing to the home screen |
| `sw.js` | Service worker for offline use |
| `icons/` | App icons |
