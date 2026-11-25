# Amazon Selection Workflow — 亚马逊选品研究

Static single-file product-selection website for Amazon US / FBA.

**Live demo:**
https://chenqinhong63.github.io/amazon-selection-workflow/

## What it is

A product-selection workflow in four steps:

- **Step 0 — Store Profile:** target market United States, category All Categories, price band 20-60, target gross margin 35%-45%, monthly sales 300-2000, monthly search volume 1000-10000, reviews 50-800, FBA, New Store, target audience, supply-chain advantages, constraints, notes. Saved to `localStorage`, reusable.
- **Step 1 — Discovery:** one keyword → 20 candidates, grouped as core category, material, scene, function, multilingual/spelling variants. Rule-based expansion, transparent word lists — **not search-volume data**. One-click demo example loads the 20 candidates for `insulated water bottle`.
- **Step 2 — Six-dimension filter:** defaults min price $9.99, max $39.99, min monthly sales 300, max reviews 1000, min rating 4.0, min profit margin 25%. Each candidate has editable data fields. A candidate passes only if **all provided values** meet the thresholds. If retained > 8, the user must manually tick ≤ 8 to proceed.
- **Step 3 — Trend + Profit + Competitors:** trend table, profit calculator (net = price − product cost − FBA fee − price × referral %; break-even shown), competitor/risk checkboxes.
- **Step 4 — Final report:** trend table, profit table, risks, ranked recommendations (推进 / 推荐 / 观望) with transparent rules, plus "insufficient data — do not promote". Copy / Print-PDF / Download Markdown / save run to localStorage history.
- **Second entry form:** name (required) + Description textarea.

## Data rule — read this first

This site has **no live connection** to SellerSprite, Keepa, Amazon, or any data provider. It never claims one. All numbers are entered by the user or imported via CSV.

- A dimension with no data entered is "unknown" — the candidate is marked **insufficient data** and does **not** pass silently.
- If **all** data is blank, ranking is blocked with a warning: "No data entered — cannot rank. Enter real data from SellerSprite / Keepa / Amazon, or import a CSV."
- Only candidates with **both** trend and profit data are ranked.
- Demo data is labelled as format demo only, not real search volume.

## How to use

1. Open `index.html` (or the Pages URL). Fill in Step 0 once; it is saved locally.
2. Step 1: enter a keyword, or click "Load demo example".
3. Step 2: confirm the six thresholds, then fill real data per candidate (or import a CSV — download the template from the page), then Run Filter. If retained > 8, tick ≤ 8 and confirm.
4. Step 3: check the trend table, enter product cost / FBA fee / referral % per candidate, tick risks.
5. Step 4: Generate Report → Copy / Print-PDF / Download Markdown / Save Run.

CSV columns: `keyword, price, monthly_sales, rating, reviews, profit_margin_pct, trend_avg_search, trend_latest, trend_peak, data_points`

## Deploy to GitHub Pages

Repo: `amazon-selection-workflow` under `chenqinhong63` (public).

```bash
git add index.html README.md TESTING.md .nojekyll
git commit -m "Amazon selection workflow"
git branch -M main
git push origin main
```

Then in the repo: **Settings → Pages → Deploy from a branch → main / (root)**.
Site URL: https://chenqinhong63.github.io/amazon-selection-workflow/

`.nojekyll` is included so Pages serves the site as-is. No build step, no backend, no secrets, no API keys. Works offline from a static host.

## Files

- `index.html` — the whole app (CSS + JS inline, single file)
- `README.md` — this file
- `TESTING.md` — what was tested and what was not
- `.nojekyll` — empty, disables Jekyll on Pages

## Disclaimer

This is a selection-workflow demo. It does not promise sales, ranking, or platform approval. Data is entered by the user and should be verified.

MIT License.
