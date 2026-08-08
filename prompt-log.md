# Prompt Log

This file documents prompts used with AI tools while developing this portfolio.

## Bio Prompt

Draft a personal and authentic professional bio for Derek Sheerer, a Finance student at the University of Hawaiʻi at Mānoa graduating in Fall 2026, highlighting his interests in entrepreneurship and business, the outdoor and surf industry, and hospitality and customer service.

## Stage 2 – Model Specification

**Prompt:**

Draft a complete Stage 2 FX hedging specification using the assignment requirements and named-range contract.

**AI Draft Issue:**

The initial draft did not clearly separate the money-market hedge into three calculation steps and did not explicitly state the ACT/360 day-count convention.

**Revision Made:**

I updated the specification by separating the money-market hedge into the required three steps (borrow, convert, invest), added the ACT/360 convention to the assumptions, and included the covered interest rate parity validation check so the workbook can be audited properly.

## Stage 3 – AI Build and Audit

**Prompt:**
Built the workbook from the Stage 2 specification using ChatGPT Work (Codex).

**Issue Found:**
The initial workbook contained invalid merged-cell records and compatibility issues that caused Excel repair warnings and formula errors.

**Revision Made:**
Rebuilt the workbook without merged cells, corrected the executive summary reference, replaced incompatible validation checks, and verified the workbook opened cleanly in Microsoft Excel with passing validation checks.

## Stage 4 – Live Market Data, Workbook Population, and Audit

**Prompt:**
Complete Stage 4 using the existing Stage 3 EUR receivable workbook, replace placeholder inputs with August 7, 2026 market-close data, document sources and proxy choices, calculate the forward through covered interest parity when necessary, populate the named input cells, and verify the recalculated workbook.

**AI Assistance:**
AI assisted with researching the EUR/USD close, the U.S. one-year Treasury yield, and the latest available ECB one-year AAA euro-government yield; calculating the CIP-implied forward; populating and auditing the existing named-range input cells; checking the sensitivity table and chart; and drafting the market-data memo.

**Issue Found:**
After the existing workbook was imported, the Sensitivity scatter chart lost its settlement-rate x-value references and displayed point indices instead of exchange rates. The ECB's August 7 one-year AAA yield observation was also not yet available at retrieval, so the latest published August 6 observation had to be disclosed as the euro-rate proxy.

**Revision Made:**
Rebuilt only the chart object against the existing formula-driven sensitivity ranges, preserved all model formulas, used the official August 7 U.S. Treasury observation and the latest available ECB one-year euro-government observation, calculated `F0_in` through CIP at full precision, and verified the candidate in Microsoft Excel with a passing parity check and zero formula errors. The FX Hedging Lab was not directly accessible, so the memo includes explicit inputs and outputs for a manual cross-check rather than claiming completion.
