# Store commission dashboard — iORA & TRT

A single-page dashboard showing commission revenue, payout and orders by outlet
for iORA SG, iORA MY, TRT SG and TRT MY, across 2025 and 2026 (to July).

## Files

| File | What it is |
|---|---|
| `index.html` | The dashboard. Brand logos and a fallback copy of the data are baked in, so it works even opened straight from disk. |
| `commission-data.json` | All the figures. Replace this to update the dashboard. |
| `vercel.json` | Tells Vercel never to cache the data file, so updates appear immediately. |

## Putting it on Vercel

**Option A — drag and drop (2 minutes, no tools)**

1. Put these three files in a folder on your machine.
2. Go to vercel.com, sign in, and choose **Add New → Project**.
3. Drag the folder onto the upload area. Vercel serves `index.html` automatically.
4. Choose a name — you get a URL like `iora-commission.vercel.app` to share.

**Option B — Git, so updates are one commit (recommended for a team)**

1. Create a repository and add the three files.
2. In Vercel: **Add New → Project → Import** that repository. Accept the defaults;
   there is no build step.
3. Every push to the main branch redeploys within seconds.

## Updating the numbers

The dashboard reads `commission-data.json` at page load. To refresh:

- **Option A:** re-upload the folder with the new `commission-data.json`.
- **Option B:** commit the new `commission-data.json` and push.

Nothing in `index.html` needs to change. It also carries an embedded copy of the
data as a fallback, so the file still works if you open it straight from disk —
but the JSON file wins whenever it loads, so that is the one to update.

## About "live"

This is a published snapshot, not a live feed. It updates when you publish new
data, which for a monthly commission cycle is usually what you want — the numbers
stay stable while your team is looking at them.

If you later want it to update on its own, the step up is a small Vercel
Serverless Function that queries Shopify and the commission workbook on a
schedule and writes `commission-data.json`. That needs a Shopify Admin API token
kept in Vercel's environment variables, never in the repository.

## Access

Vercel projects are public by default. Anyone with the URL can read the figures.
On a Pro plan you can turn on **Deployment Protection** (Vercel Authentication)
so only your team can open it. Worth doing — this is internal commission data.

## Design notes

iORA carries a light neutral grey, The Restyle Trait a gold; Singapore and Malaysia
within each brand take slightly different tones of the same colour. The wordmark
sits large in the header and on each selector button, and the page title names the
brand: "iORA SG's store commission".

The layout is deliberately plain and ledger-like. Two visuals earn their place:

- **Sparkline** beside the headline figure, showing the shape of the period.
- **Best performing / Least performing** as three classic cards each — a serif rank
  numeral, the outlet, its revenue, and orders plus share beneath a hairline rule.
  The leader takes the brand accent; the least-performing cards a thin red edge.

Everything else is a clean ranked table of every outlet, sortable by any column.

## Data notes

- 2026 covers January to July.
- Singapore brands are in SGD, Malaysia brands in MYR. Totals are never mixed
  across currencies; pick a brand to see its figures.
- Commission revenue is the value of orders an outlet referred. Payout is the
  incentive that outlet earned. Share of total sales compares commission revenue
  with the brand's all-channel sales for the same period.
- Source: ECM store incentive records.
