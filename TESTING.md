# TESTING.md — 测试记录

Date: 2026-11-25. Tester: headless Node harness (`/tmp/test-asw.js`,
`/tmp/test-asw2.js` — DOM stubs, not a real browser) + `python3 -m http.server`.

## Tested — passed

1. **JS syntax**: `node --check` on the extracted `<script>` — OK.
2. **No secrets / no live claims**: grep found no password, email, API key in
   `index.html` / `README.md`; no external `http(s)://` references in the page
   (fully self-contained, works offline).
3. **Demo example (insulated water bottle)**: one click loads exactly 20
   candidates, including the misspelled `water bottoe` / `water bootle` and
   the Spanish variants — matching the demo example.
4. **Data gate — blank data blocks ranking**: with all data blank, Run Filter
   shows the blocking warning (Chinese + "No data entered — cannot rank"),
   selects nothing, produces no ranking. This is the data-gate rule: no data, no ranking.
5. **Demo data → filter**: filling the demo snapshot retains 7/20,
   13 marked "数据不足" (insufficient data), ≤ 8 so it proceeds directly.
6. **Profit + report**: demo profit costs compute live; final report ranks
   `stainless steel water bottle with handle` #1 as 推进 (trend 1.07,
   net $8.44, margin 42.2% — matching the demo $8.44 / 42.2%).
   Report does not claim an opportunity score.
7. **Insufficient-data report path**: a selected candidate with no trend /
   profit data appears under "数据不足 — 不推进" with the reason named
   (e.g. 缺趋势数据), and is not ranked.
8. **> 8 branch rule**: with 10 candidates passing, auto-selection is empty
   and the panel requires manual ticking of ≤ 8 with a Confirm button.
9. **Generic keyword expansion**: `yoga mat` yields 20 candidates and the
   output is labelled rule-based expansion, not search data.
10. **HTTP serving**: `python3 -m http.server` serves `index.html` with
    HTTP 200 and `README.md` with HTTP 200.

## NOT tested

- **Real browser rendering / clicking**: no headless Chromium run in this
  session (subagent has no live-browser access). Layout on mobile widths,
  the Print-to-PDF dialog, the Copy-to-clipboard permission prompt, and the
  CSV file-picker were not exercised in a real browser. The harness stubs
  `scrollIntoView`, `clipboard`, `Blob`/`URL.createObjectURL` and the file
  input, so a typo in a real-browser-only API would not have been caught.
  → Before publishing, open the Pages URL in a real browser and click
  through once: demo example → Run Filter → Generate Report → Print.
- **CSV import with a real file**: parsing logic is exercised only via the
  template format in code; a real `.csv` file-pick was not run.
- **localStorage persistence across reloads** in a real browser (stubbed in
  the harness; `saveProfile` / `saveRun` / `renderRuns` logic paths ran,
  but not against a real browser profile).
- **GitHub Pages deployment**: not published (per instructions, publishing
  is the parent's next step). The Pages URL is therefore unverified until
  the repo is created and Pages is enabled.
- **Real SellerSprite / Keepa / Amazon data**: intentionally not connected.
  Any numbers a user sees after "Fill demo data" are labelled demo data —
  format demo only, not real search volume.
