# Amazon Selection Workflow — 亚马逊选品研究

Static single-file product-selection website for Amazon US / FBA, replicating the
selection workflow reverse-engineered from the public RexiFlow demo on 2026-11-25.

**Live demo (after Pages is enabled):**
https://chenqinhong63.github.io/amazon-selection-workflow/

## What it is

A faithful replica of the *workflow and fields* — not of RexiFlow's data, brand,
or backend:

- **Step 0 — Store Profile** (`/research/store-profile` fields): target market
  United States, category All Categories, price band 20-60, target gross margin
  35%-45%, monthly sales 300-2000, monthly search volume 1000-10000, reviews
  50-800, FBA, New Store, target audience, supply-chain advantages,
  constraints, notes. Saved to `localStorage`, reusable.
- **Step 1 — Discovery** (`discover_keywords`): one keyword → 20 candidates,
  grouped exactly like the real run: core category, material/insulation, scene,
  function, multilingual/spelling variants. Rule-based expansion, transparent
  word lists — **not search-volume data**. One-click demo example loads the
  exact 20 candidates from the 2026-11-25 `insulated water bottle` run.
- **Step 2 — Six-dimension filter** (`filter_candidates`): defaults min price
  $9.99, max $39.99, min monthly sales 300, max reviews 1000, min rating 4.0,
  min profit margin 25%. Each candidate has editable data fields. A candidate
  passes only if **all provided values** meet the thresholds. If retained
  > 8, the user must manually tick ≤ 8 to proceed (the real RexiFlow branch rule).
- **Step 3 — Trend + Profit + Competitors**: trend table, profit calculator
  (net = price − product cost − FBA fee − price × referral %; break-even shown),
  competitor/risk checkboxes. Profit with missing cost data is marked
  failed/empty, like the real run did for `metal insulated water bottle`.
- **Step 4 — Final report**: trend table, profit table, risks, ranked
  recommendations (推进 / 推荐 / 观望) with transparent rules, plus
  "insufficient data — do not promote". Copy / Print-PDF / Download Markdown /
  save run to localStorage history.
- **Second entry form** (`/research/new`): name (required) + Description textarea.

## Data honesty warning — read this first

In the 2026-11-25 logged-in RexiFlow run, the report was generated while the
underlying data was empty:

- 8 product searches → **0 results**; 3 ASIN detail fetches failed;
  0 reviews; 0 keywords on reverse lookup.
- Trend numbers were near-identical: average search 101,261–101,284 and peak
  **exactly 202,611 for all 7** keywords — suspected placeholder data.
- Opportunity Score +34% and 12 risk signals **never appeared** in the real flow.
- The pricing page was a generic SaaS template.

This site fixes that with a **data gate**:

- A dimension with no data entered is "unknown" — the candidate is marked
  **insufficient data** and does **not** pass silently.
- If **all** data is blank, ranking is blocked with a warning:
  "No data entered — cannot rank. Enter real data from SellerSprite / Keepa /
  Amazon, or import a CSV."
- Only candidates with **both** trend and profit data are ranked.
- Demo data is labelled as the 2026-11-25 snapshot, including its suspect
  trend numbers — format demo only, not real search volume.

**This site has no live connection** to Pangolinfo, SellerSprite, Keepa,
ChatGPT, or Amazon. It never claims one. All numbers are entered by the user
or imported via CSV.

## How to use

1. Open `index.html` (or the Pages URL). Fill in Step 0 once; it is saved locally.
2. Step 1: enter a keyword, or click "Load RexiFlow demo example".
3. Step 2: confirm the six thresholds, then fill real data per candidate
   (or import a CSV — download the template from the page), then Run Filter.
   If retained > 8, tick ≤ 8 and confirm.
4. Step 3: check the trend table, enter product cost / FBA fee / referral %
   per candidate, tick risks.
5. Step 4: Generate Report → Copy / Print-PDF / Download Markdown / Save Run.

CSV columns: `keyword, price, monthly_sales, rating, reviews,
profit_margin_pct, trend_avg_search, trend_latest, trend_peak, data_points`

## Deploy to GitHub Pages

Repo suggestion: `amazon-selection-workflow` under `chenqinhong63` (public).

```bash
git init
git add index.html README.md TESTING.md .nojekyll
git commit -m "Amazon selection workflow (RexiFlow reverse-engineering, 2026-11-25)"
git branch -M main
git remote add origin https://github.com/chenqinhong63/amazon-selection-workflow.git
git push -u origin main
```

Then in the repo: **Settings → Pages → Deploy from a branch → main / (root)**.
Site URL: https://chenqinhong63.github.io/amazon-selection-workflow/

`.nojekyll` is included so Pages serves the site as-is. No build step,
no backend, no secrets, no API keys. Works offline from a static host.

## Files

- `index.html` — the whole app (CSS + JS inline, single file)
- `README.md` — this file
- `TESTING.md` — what was tested and what was not
- `.nojekyll` — empty, disables Jekyll on Pages

## Attribution / disclaimer

Workflow reverse-engineered from the public RexiFlow demo on 2026-11-25.
Not affiliated with RexiFlow, Amazon, Pangolinfo, SellerSprite, or Keepa.
Field names are short factual labels; no logo, brand, or copyrighted text
was copied. Full reverse-engineering record:
`workspace/research/rexiflow-selection-reverse-engineering.md`.

MIT License.
