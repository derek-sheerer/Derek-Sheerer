# Stage 2 EUR Receivable Model — Build Audit

**Date:** 2026-08-07  
**Author:** Derek Sheerer  
**Workbook:** `models/builds/2026-08-07-sheerer-eur-receivable-model.xlsx`

## Scope

This audit documents structural and formula issues identified while building and testing the Stage 2 EUR receivable hedge model. The final workbook was checked at the XLSX package level, rendered for visual review, and opened and recalculated in Microsoft Excel.

## Finding 1 — Invalid merge-cell records

### What was checked

- The initial workbook was opened in Microsoft Excel.
- Excel's repair log was reviewed.
- Worksheet XML files for all nine sheets were checked for `mergeCells` and `mergeCell` records.

### What was found

Excel detected invalid merge-cell records in the initial workbook and repaired all nine worksheet files on open. Removing those records during repair disrupted workbook behavior and contributed to failed status and summary outputs.

### What was done to fix or verify it

- The workbook was rebuilt without merged cells.
- Title bands, section headers, subtitles, and note blocks were reformatted using normal unmerged cells, fills, borders, and text flowing across empty cells.
- The final XLSX archive passed an integrity test.
- All nine worksheet XML files were scanned and confirmed to contain no merge-cell records.
- The regenerated workbook opened in Microsoft Excel without a repair interruption.

## Finding 2 — Incorrect executive-summary money-market reference

### What was checked

- Each executive-summary formula on the Cover sheet was reconciled to the corresponding strategy output.
- The money-market summary link was traced to the Money Market Hedge sheet.

### What was found

The initial executive summary referenced the money-market label cell instead of the final USD proceeds cell. The Cover formula pointed to `'Money Market Hedge'!B12`; the correct calculated output is in `'Money Market Hedge'!C12`.

### What was done to fix or verify it

- The Cover formula was corrected to reference `'Money Market Hedge'!C12`.
- A reconciliation validation confirms that all Cover summary outputs equal their underlying strategy calculations.
- Microsoft Excel recalculated the corrected money-market summary to approximately USD 5,085,219.51, and the summary validation passed.

## Finding 3 — Incompatible `ISFORMULA` validation formulas

### What was checked

- Formula-error scans and validation outputs were reviewed after the first build.
- The formula engine results for the Section 7 checks were compared with Microsoft Excel behavior.

### What was found

Validation formulas using `ISFORMULA` returned compatibility errors in the build environment. This caused the summary-formula and automatic-update checks to return errors rather than valid pass/fail results.

### What was done to fix or verify it

- The `ISFORMULA` tests were replaced with compatible reconciliation checks.
- The replacement checks compare summary outputs with their source calculations and compare key strategy and sensitivity outputs with independently stated expected formulas.
- The final workbook returned `PASS` for both checks in Microsoft Excel.

## Finding 4 — Named ranges exported as relative references

### What was checked

- The ten required named ranges were inspected in the generated XLSX package.
- Their values were read after Microsoft Excel performed a full recalculation.
- Failing Excel formulas were traced cell by cell.

### What was found

The first unmerged rebuild exported names such as `'Inputs'!B9` as relative references. Microsoft Excel shifted those references according to the formula location, causing incorrect named-range values, blank or invalid calculated outputs, and failed validation checks.

### What was done to fix or verify it

- All ten names were rewritten as explicit absolute references, such as `='Inputs'!$B$9`.
- Microsoft Excel then returned the correct values for all named inputs and all dependent calculations.
- The named-range mapping validation passed.

## Final Verification

- Microsoft Excel opened the final workbook with alerts enabled and without a repair interruption.
- Excel performed a full recalculation.
- The Cover model status returned `PASS`.
- All six Section 7 validation rows returned `PASS`.
- The overall validation status returned `PASS`.
- An Excel-native error sweep across every populated sheet returned zero formula errors.
- The final XLSX archive passed its package-integrity test and contains no merge-cell records.
