# Stage 2 – Model Specification
## EUR Receivable Hedge Model

### 1. Problem Statement

The firm expects to receive EUR 4,500,000 in one year from a European customer. Because the payment will be converted into U.S. dollars, a decline in the EUR/USD exchange rate before settlement would reduce the USD proceeds received. This workbook will compare forward, money-market, and option hedging strategies so management can evaluate the tradeoffs between locking in a fixed exchange rate and maintaining upside participation. All placeholder market data shown below is indicative and will be replaced with live market data during Phase 4.

---

## 2. Inputs – Named-Range Contract

| Named Range | Placeholder Value* | Unit | Phase 4 Source |
|-------------|-------------------|------|----------------|
| FC_AMT | 4,500,000 | EUR | Scenario assignment |
| S0_in | 1.10 | USD/EUR | Live spot market |
| F0_in | 1.11 | USD/EUR | Live forward quote |
| R_USD | 5.30% | Annual % (ACT/360) | Federal Reserve H.15 |
| R_FC | 2.50% | Annual % (ACT/360) | ECB reference rate |
| K_PUT | 1.10 | USD/EUR | Option market |
| K_CALL | 1.10 | USD/EUR | Option market |
| PREM_PUT | 0.03 | USD per EUR | Option market |
| PREM_CALL | 0.03 | USD per EUR | Option market |
| T_DAYS | 360 | Days | Scenario assignment |

*All placeholder values are indicative and will be replaced with live market data during Phase 4.

---

## 3. Tab Architecture

### Cover
Project title, student name, scenario summary, and date.

### Legend/Key
Definitions of named ranges, units, assumptions, and color coding.

### Inputs
All editable assumptions and market data.

### Forward Hedge
Forward hedge calculations and locked USD proceeds.

### Money Market Hedge
Borrow, convert, invest, and final proceeds.

### Option Hedge
Put and call option calculations and net proceeds.

### Sensitivity
Sensitivity table and comparison chart.

### Notes & Assumptions
Documentation of assumptions and modeling choices.

---

## 4. Assumptions & Constraints

- Interest rates use the ACT/360 day-count convention.
- Placeholder values are indicative and replaced with live market data during Phase 4.
- Transaction costs, taxes, bid-ask spreads, and credit risk are ignored.
- Exchange rates are quoted as USD per EUR.
- Option premiums are paid upfront and deducted from proceeds.
- Forward contracts require no upfront premium.
- Money-market borrowing and investing occur immediately.
- Covered interest rate parity is expected to hold within normal rounding.

---

## 5. Calculation Flow

### Forward Hedge

USD Proceeds = FC_AMT × F0_in

This locks the exchange rate regardless of the future spot rate.

### Money-Market Hedge

**Step 1**

Borrow foreign currency today:

Borrow = FC_AMT ÷ (1 + R_FC × T_DAYS / 360)

**Step 2**

Convert borrowed euros into dollars:

USD_now = Borrow × S0_in

**Step 3**

Invest the dollars until settlement:

USD Proceeds = USD_now × (1 + R_USD × T_DAYS / 360)

The three calculations should remain separate so they are easy to audit.

### Covered Interest Rate Parity

F_implied = S0_in × (1 + R_USD × T_DAYS / 360) ÷ (1 + R_FC × T_DAYS / 360)

F_implied should approximately equal F0_in.

### Put Option

USD Proceeds = FC_AMT × max(S_T, K_PUT) − FC_AMT × PREM_PUT

The put establishes a minimum exchange rate while still allowing upside if the euro appreciates.

### Call Option

Include the call option using the same framework, showing premium cost and participation payoff.

---

## 6. Sensitivity Plan

Analyze settlement exchange rates from 95% of S0_in to 105% of S0_in in 1% increments.

Calculate:

- Unhedged proceeds
- Forward hedge proceeds
- Money-market hedge proceeds
- Put option proceeds

Display one comparison chart showing USD proceeds versus settlement exchange rate so the CFO can compare downside protection and upside potential.

---

## 7. Validation Rules

The workbook should pass the following checks:

- Forward hedge proceeds and money-market hedge proceeds should differ only by rounding.
- Covered interest rate parity should hold.
- No formula cells should return errors.
- Every summary output should reference formulas instead of hard-coded values.
- Named ranges should be used consistently.
- All outputs should update automatically when inputs change.

---

## 8. Outputs

The workbook will display:

- Forward hedge USD proceeds
- Money-market hedge USD proceeds
- Put option proceeds
- Call option comparison
- Unhedged proceeds
- Implied forward rate
- Covered interest parity check
- Sensitivity table
- Strategy comparison chart
- Executive summary