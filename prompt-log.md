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