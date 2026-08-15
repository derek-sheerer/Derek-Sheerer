# CFO Decision Memo — EUR Receivable Hedge Recommendation

**To:** Chief Financial Officer

**From:** Derek Sheerer

**Date:** 2026-08-14

**Subject:** Recommended hedge for EUR 4.5 million receivable due in 360 days

## Executive Decision

Use a one-year forward contract as the primary hedge for the full EUR 4,500,000 receivable. At the verified forward rate of 1.172323293235 USD/EUR, the contract locks approximately **USD 5,275,454.82** at settlement with no upfront premium. The forward provides the same modeled proceeds as the money-market hedge under covered interest parity, but it avoids the money-market strategy's immediate borrowing, currency conversion, investment, and balance-sheet administration.

If management places a high value on retaining upside from euro appreciation, use the EUR put as the flexible alternative. The put requires a **USD 135,000** premium and establishes a verified net floor of **USD 5,066,550** while preserving gains when the settlement spot rate exceeds the 1.1559 USD/EUR strike. The call strategy should not influence the decision because its position and payoff were not adequately defined in the Stage 2 specification, and the workbook's “Long EUR Call” label conflicts with its formula.

## A. Exposure Summary

The company expects to receive EUR 4,500,000 in 360 days. Because the receivable will ultimately be converted into U.S. dollars, the company is exposed to a decline in EUR/USD. With exchange rates quoted as USD per EUR, a lower settlement rate means fewer dollars for the same euro receivable. Leaving the position unhedged therefore exposes operating cash flow to currency movements that are unrelated to the underlying customer transaction.

The live-data model uses an August 7, 2026 EUR/USD close of 1.1559, a one-year USD rate of 4.01%, and a one-year EUR proxy rate of 2.5529047267%. In the absence of a reliable directly accessible one-year forward quote, the Stage 4 analysis calculated a full-precision covered-interest-parity forward of 1.172323293235 USD/EUR. The model applies a 360-day ACT/360 convention and ignores transaction costs, taxes, bid-ask spreads, credit risk, and financing of option premiums.

The three decision scenarios are:

| Scenario | S_T (USD/EUR) | Currency interpretation |
|---|---:|---|
| 95% of current spot | 1.098105 | EUR depreciates 5% |
| 100% of current spot | 1.155900 | EUR unchanged |
| 105% of current spot | 1.213695 | EUR appreciates 5% |

These scenarios are not forecasts. They are controlled sensitivity cases used to compare the risk and payoff structure of each strategy.

## B. Hedge Outcomes

The independently validated proceeds are:

| Strategy | 95% S_T | 100% S_T | 105% S_T | Upfront/explicit cost | Primary characteristic |
|---|---:|---:|---:|---:|---|
| Forward | $5,275,454.82 | $5,275,454.82 | $5,275,454.82 | $0 | Fixed proceeds |
| Money market | $5,275,454.82 | $5,275,454.82 | $5,275,454.82 | No option premium | Fixed proceeds; three transactions |
| Put option | $5,066,550.00 | $5,066,550.00 | $5,326,627.50 | $135,000 premium | Floor plus appreciation upside |
| Unhedged | $4,941,472.50 | $5,201,550.00 | $5,461,627.50 | $0 | Full downside and upside |

The forward and money-market hedges are economically equivalent in the model. The money-market sequence is to borrow EUR 4,387,979.07 today, convert it into USD 5,072,065.01 at spot, and invest the dollars to produce USD 5,275,454.82 at settlement. The future EUR receivable repays the euro borrowing. Although this result is valid, it requires more operational steps and may use borrowing capacity or affect financial-statement presentation.

The forward produces the same USD 5,275,454.82 through one contractual exchange at maturity. It exceeds the unhedged result by approximately USD 333,982.32 in the 95% scenario and USD 73,904.82 in the unchanged-spot scenario. If the euro appreciates 5%, however, the forward gives up USD 186,172.68 relative to remaining unhedged because the company must exchange at the contracted rate.

The put costs USD 135,000, calculated as EUR 4,500,000 multiplied by the 0.03 USD/EUR premium. At or below the 1.1559 strike, it produces net proceeds of USD 5,066,550. At the 95% settlement rate, this is USD 125,077.50 more than the unhedged position, but USD 208,904.82 less than the forward. At the 105% settlement rate, the put participates in euro appreciation and produces USD 5,326,627.50—USD 51,172.68 more than the forward, but still USD 135,000 less than the unhedged position because of the premium.

## C. Sensitivity Interpretation

The sensitivity analysis highlights the central tradeoff between certainty and participation.

The forward and money-market lines remain flat across settlement rates because both lock the same effective exchange rate. That stability is valuable when the primary objective is budgeting certainty, protection of operating margins, or assurance that a known dollar cash requirement will be funded.

The unhedged position changes dollar-for-dollar with EUR/USD. A 5% depreciation reduces proceeds to USD 4,941,472.50, while a 5% appreciation increases proceeds to USD 5,461,627.50. This creates the greatest upside but also the greatest downside and leaves the firm's cash outcome dependent on an exchange-rate movement outside management's core business.

The put creates an asymmetric result. The maximum modeled downside is the strike value less the premium, or USD 5,066,550, while favorable EUR appreciation remains available after paying the premium. The put overtakes the forward only when:

```text
FC_AMT × S_T − FC_AMT × PREM_PUT > FC_AMT × F0_in

S_T > F0_in + PREM_PUT
S_T > 1.172323293235 + 0.03
S_T > 1.202323293235 USD/EUR
```

Thus, the euro must finish above approximately 1.20232 USD/EUR—about 4.0% above the current spot—before the put's net proceeds exceed the forward's locked proceeds. The 105% scenario clears this threshold; the base scenario does not.

The option premium should therefore be viewed as the price of flexibility. Management pays USD 135,000 to retain appreciation upside and accepts a floor that is USD 208,904.82 below the forward outcome. That trade may be justified when management has a constructive view on the euro, values participation, or wants protection without committing to a fixed forward exchange. It is less attractive when certainty and maximum protected proceeds are the dominant objectives.

## D. Recommendation

Execute a one-year forward sale of EUR 4,500,000 for USD at the modeled rate of 1.172323293235 USD/EUR, subject to obtaining and approving an executable dealer quote at the time of transaction. The resulting modeled settlement proceeds are USD 5,275,454.82.

The forward is the strongest primary recommendation for four reasons:

1. **It provides the highest guaranteed modeled proceeds.** The forward locks USD 208,904.82 more than the put's guaranteed floor.
2. **It requires no upfront option premium.** The company avoids the USD 135,000 cash cost of preserving upside.
3. **It is operationally simpler than the money-market hedge.** It avoids immediate EUR borrowing, spot conversion, USD investment, and repayment administration while producing the same modeled settlement value.
4. **It directly matches the exposure.** The notional and maturity can be aligned with the known EUR receivable, creating a straightforward hedge relationship.

Before execution, treasury should confirm the receivable amount and timing, obtain a current executable forward quote, evaluate counterparty and credit terms, and document the hedge under the company's treasury and accounting policies. The Stage 4 forward is a CIP-derived model input rather than a guaranteed tradable quote, so the actual contracted proceeds may differ because of market movement, dealer spreads, credit adjustments, and exact settlement conventions.

If management prefers upside participation and accepts its cost, the approved alternative is a one-year EUR put with a 1.1559 USD/EUR strike and EUR 4,500,000 notional. Under the model, it guarantees USD 5,066,550 net of the USD 135,000 premium. Treasury should obtain a current option quote before execution because the model retains an assigned premium rather than a live option-market premium.

The ambiguous call output should be excluded from strategy selection. The specification does not adequately define the call position, and the workbook labels the strategy as long while subtracting its payoff. Using that result could misstate the economics of the proposed hedge.

## E. Executive Justification

The recommended forward converts a material and avoidable foreign-exchange uncertainty into a known dollar cash inflow. It protects the firm from a weaker euro, supports cash forecasting, and provides USD 5,275,454.82 in each tested scenario. The money-market hedge validates the forward economically but adds transactions without improving proceeds. The put preserves upside but requires a USD 135,000 premium and lowers the guaranteed floor to USD 5,066,550. Remaining unhedged offers the most favorable result only if the euro appreciates, while exposing the company to proceeds as low as USD 4,941,472.50 in the tested downside scenario.

For a known one-year receivable, the forward offers the clearest balance of protection, value, and execution simplicity. The put remains a credible alternative if management deliberately chooses to pay for upside participation. The decision should not rely on the call until its specification and workbook implementation are corrected and revalidated.

## Decision Record

**Primary recommendation:** Full-notional one-year forward hedge.

**Modeled locked proceeds:** USD 5,275,454.82.

**Flexible alternative:** EUR put with USD 135,000 premium and USD 5,066,550 modeled floor.

**Excluded from recommendation:** Call strategy pending specification clarification and workbook correction.

This recommendation is based on the verified Stage 4 inputs and Stage 5 validation. It is an analytical project conclusion, not an executable market quotation.
