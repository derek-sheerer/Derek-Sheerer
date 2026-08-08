# Stage 4 Market-Data Memo — EUR Receivable Hedge

**Scenario:** EUR 4,500,000 receivable due in 360 days  
**Market-data date:** 2026-08-07 market close  
**Primary research retrieval:** 2026-08-08 06:41:31 UTC / 2026-08-07 20:41:31 HST  
**EUR/USD close-source retrieval:** 2026-08-08 06:46:17 UTC / 2026-08-07 20:46:17 HST

## Market Inputs

| Named range/input | Value loaded | Source | Retrieval timestamp | Proxy/computation/assumption notes |
|---|---:|---|---|---|
| `FC_AMT` | EUR 4,500,000 | Original scenario and Stage 3 workbook | Not applicable — retained scenario input | Unchanged from the assigned EUR receivable. |
| `S0_in` | 1.1559 USD/EUR | Investing.com, EUR/USD Historical Data: https://www.investing.com/currencies/eur-usd-historical-data | 2026-08-08 06:46:17 UTC | August 7 daily closing price. The ECB's earlier 14:15 CET reference rate was 1.1535 and was used as an official-source cross-check: https://data-api.ecb.europa.eu/service/data/EXR/D.USD.EUR.SP00.A?startPeriod=2026-08-07&endPeriod=2026-08-07&format=csvdata |
| `F0_in` | 1.172323293235 USD/EUR | Calculated in this memo from `S0_in`, `R_USD`, `R_FC`, and `T_DAYS` | 2026-08-08 06:46:17 UTC | No reliable directly accessible 1-year EUR/USD forward quote was used. Full-precision CIP value was loaded so forward and money-market proceeds reconcile without a rounding failure. |
| `R_USD` | 4.01% | U.S. Department of the Treasury, Daily Treasury Par Yield Curve Rates XML feed: https://home.treasury.gov/resource-center/data-chart-center/interest-rates/pages/xml?data=daily_treasury_yield_curve&field_tdr_date_value_month=202608 | 2026-08-08 06:41:31 UTC | Official August 7, 2026 1-year constant-maturity Treasury yield. Used as the one-year USD government-rate proxy. |
| `R_FC` | 2.5529047267% | ECB Data Portal, AAA euro-area government-bond 1-year spot-rate series `YC.B.U2.EUR.4F.G_N_A.SV_C_YM.SR_1Y`: https://data-api.ecb.europa.eu/service/data/YC/B.U2.EUR.4F.G_N_A.SV_C_YM.SR_1Y?startPeriod=2026-08-01&endPeriod=2026-08-07&format=csvdata | 2026-08-08 06:41:31 UTC | Latest official observation available as of the August 7 close was August 6, 2026. The August 7 observation had not yet been published. Used transparently as the latest-available one-year EUR government proxy. |
| `K_PUT` | 1.1559 USD/EUR | At-market strike assumption based on `S0_in` | 2026-08-08 06:46:17 UTC | Set equal to the August 7 EUR/USD close under the scenario's at/near-spot convention. No live option quote was substituted. |
| `K_CALL` | 1.1559 USD/EUR | At-market strike assumption based on `S0_in` | 2026-08-08 06:46:17 UTC | Set equal to the August 7 EUR/USD close under the scenario's at/near-spot convention. No live option quote was substituted. |
| `PREM_PUT` | 0.03 USD/EUR | Original scenario and Stage 3 workbook | Not applicable — retained scenario assumption | Kept exactly as assigned; not replaced with a live option quote. |
| `PREM_CALL` | 0.03 USD/EUR | Original scenario and Stage 3 workbook | Not applicable — retained scenario assumption | Kept exactly as assigned; not replaced with a live option quote. |
| `T_DAYS` | 360 days | Original scenario and Stage 3 workbook | Not applicable — retained scenario input | Unchanged; the workbook applies its ACT/360 convention. |

## USD and EUR Interest-Rate Proxy Rationale

### USD proxy

The U.S. Treasury's 1-year constant-maturity Treasury yield was selected because it is an official, daily, one-year U.S. government benchmark and matches the hedge's one-year horizon. Treasury states that constant-maturity yields are derived from the daily par yield curve using indicative bid-side Treasury prices observed at or near 3:30 p.m. ET. The August 7 observation was 4.01%.

### EUR proxy

The ECB AAA euro-area government-bond 1-year spot-rate series was selected because it is an official, euro-denominated, one-year sovereign yield-curve measure. It matches the currency and tenor more closely than an overnight policy or money-market rate. The series uses the ECB Svensson model and is quoted as a continuously compounded annual percentage rate.

At retrieval, the ECB feed contained observations only through August 6; the latest available value was 2.5529047267%. That observation was used as the latest official one-year euro-government proxy available as of the August 7 close. The workbook applies both quoted annual proxy rates through its existing ACT/360 simple-interest convention. This is a modeling approximation and is disclosed rather than silently changing the workbook's rate convention.

## CIP-Implied Forward Calculation

No reliable directly accessible 1-year EUR/USD forward quote was used. The forward input was calculated using the required covered-interest-parity formula:

```text
F0 = S0 × (1 + R_USD × T/360) / (1 + R_FC × T/360)

F0 = 1.1559 × (1 + 0.0401 × 360/360)
              / (1 + 0.025529047267 × 360/360)

F0 = 1.172323293235 USD/EUR
```

The full-precision result was loaded into `F0_in`. The workbook displays five decimals (`1.17232`) but retains the full value so the forward and money-market strategies reconcile exactly rather than failing because of display rounding.

## Comparison With the Original Indicative Forward

The original scenario forward was 1.13005 USD/EUR. The Stage 4 CIP-implied forward is 1.172323293235 USD/EUR.

- Absolute increase: 0.042273293235 USD/EUR
- Percentage increase: 3.7408%

The main reason is the higher August 7 spot rate: 1.1559 versus the original 1.10 placeholder. The new USD-minus-EUR rate differential is about 1.4571 percentage points, narrower than the original 2.80-point placeholder differential, which offsets part of the spot-driven increase but does not eliminate it.

## Workbook Population

The Stage 3 workbook was imported and populated only through its ten existing named-range input cells on the Inputs sheet. The following items were intentionally unchanged:

- `FC_AMT` = EUR 4,500,000
- `PREM_PUT` = 0.03 USD/EUR
- `PREM_CALL` = 0.03 USD/EUR
- `T_DAYS` = 360

A before-and-after formula-map comparison returned no formula changes. All ten workbook names remained attached to their original absolute input cells.

## Structural Fixes

One structural issue appeared after the existing workbook was imported: the Sensitivity scatter chart lost its settlement-rate x-value references and displayed point indices from 0 to 10. The sensitivity formulas and values were correct, but the chart was not showing the required exchange-rate axis.

The chart object was rebuilt against the existing formula-driven ranges:

- x-values: `Sensitivity!B6:B16`
- Unhedged: `Sensitivity!C6:C16`
- Forward: `Sensitivity!D6:D16`
- Money Market: `Sensitivity!E6:E16`
- Put Option: `Sensitivity!F6:F16`

No model formulas were changed. The rebuilt chart now displays settlement rates on the x-axis and updates with `S0_in`.

## Parity and Sensitivity Verification

Microsoft Excel opened the Stage 4 candidate with alerts enabled, performed a full recalculation, and returned zero formula errors across all nine sheets.

- Covered-interest-parity status: `PASS`
- Overall model status: `PASS`
- Forward proceeds: USD 5,275,454.82
- Money-market Step 1 — borrow today: EUR 4,387,979.07
- Money-market Step 2 — convert today: USD 5,072,065.01
- Money-market Step 3 — final invested proceeds: USD 5,275,454.82
- Forward versus money-market difference: USD 0.00
- Sensitivity low rate, 95% of spot: 1.098105 USD/EUR
- Sensitivity base rate, 100% of spot: 1.155900 USD/EUR
- Sensitivity high rate, 105% of spot: 1.213695 USD/EUR
- Unhedged proceeds at the illustrative base rate: USD 5,201,550.00
- Put net proceeds at the illustrative base rate: USD 5,066,550.00

The sensitivity table recalculated around the new spot rate, and the comparison chart updated to the same 95%–105% settlement-rate range.

## FX Hedging Lab Cross-Check — Not Completed

The FX Hedging Lab could not be accessed directly during this work, so no lab-completion claim is made.

Enter these values into the lab:

| Lab input | Value |
|---|---:|
| Receivable amount | EUR 4,500,000 |
| Spot EUR/USD | 1.1559 USD/EUR |
| 1-year forward | 1.172323293235 USD/EUR |
| USD annual rate | 4.01% |
| EUR annual rate | 2.5529047267% |
| Put strike | 1.1559 USD/EUR |
| Call strike | 1.1559 USD/EUR |
| Put premium | 0.03 USD/EUR |
| Call premium | 0.03 USD/EUR |
| Time | 360 days |
| Day-count convention | ACT/360 |

Compare the lab outputs with these workbook results:

- CIP-implied forward: 1.172323293235 USD/EUR
- Forward proceeds: USD 5,275,454.82
- EUR borrowed today: EUR 4,387,979.07
- USD converted today: USD 5,072,065.01
- Money-market final proceeds: USD 5,275,454.82
- Unhedged proceeds at `S_T = S0_in`: USD 5,201,550.00
- Put net proceeds at `S_T = S0_in`: USD 5,066,550.00

If the lab uses a different rate compounding convention or rounds the forward before calculating proceeds, compare directionally and reconcile the difference to those conventions. If its call-option convention differs from the scenario-specific call formula in the workbook, do not treat that call-output difference as a workbook error without first aligning the payoff definitions.
