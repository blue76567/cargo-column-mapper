# cargo-column-mapper

Customer cargo list → your 18-column stowage table (for the "Compilation of AutoCAD-Script-Files" tool).

## Use (for everyone, no install)

1. Open https://blue76567.github.io/cargo-column-mapper/ — or download `index.html` from this repo and double-click it.
2. Drop the customer's `.xlsx` / `.csv` onto the page.
3. Check the auto-detected column mapping, fix anything wrong via the dropdowns (manual match fallback).
4. Hit **Download stowage-ready .xlsx**, paste it into your stowage sheet below the dark header row, press Create Script-File as before.

Everything runs locally in the browser. Files are never uploaded — safe for confidential customer data.

## What it maps to

Quantity, No., Port of Loading, Port of Disch., Description, Length m, Width m, Height m,
Weight mt, COG long., COG transv., Remark, Top color, Rectangle/hatch color, Layer,
Volume singel m3 (calc), Volume total m3 (calc), plot with hatch (y/n).

## Auto-detection

Header names are normalized (case/whitespace/brackets/units stripped, German umlauts folded)
and matched against EN + DE synonym lists (qty/Stk/Anzahl, length/Länge, weight/Gewicht/kg→mt, …).
Number parsing accepts `12,5` and `12.5`, `1.200,5` and `1,200.5`, trailing units (`m`, `mt`, `kg` → auto-converted to mt).
Core columns left unmapped are flagged before export; defaults apply for colors/layer/hatch/COG.

Export rules enforced (your tool's requirements): no empty lines, dots not commas in Length/Width,
all number cells filled (empty → 0 so the script macro never hits #VALUE!).

## Dev

Single self-contained file: `index.html` (only external dep: SheetJS CDN for xlsx parse/export).
No build step. To test mapping logic: `node test/mapping.test.js`.
