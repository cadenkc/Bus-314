# Caterpillar Inc. (CAT) Financial Ratio Analysis – Technical Specification

**Created by:** Caden Chew
**Updated by:** Caden Chew
**Date Created:** April 24, 2026
**Date Updated:** April 24, 2026
**Version:** 1.0
**LLM Used:** Claude (Anthropic)

**Role:** Financial Analyst / FP&A Analyst
**Audience:** CFO or Director of FP&A

**Purpose:** Provide a professional, quantitative specification documenting the Stage 2 Excel model's analytical structure for computing and interpreting 25+ accounting and performance ratios from Caterpillar Inc.'s FY2024 financial statements. This post-build spec captures what was built, what was learned, and how the model should be refined.

---

## 1. Problem Statement

Caterpillar Inc. (CAT) is a publicly traded Industrials company specializing in heavy machinery and equipment manufacturing. This specification outlines the analytical framework for computing 25+ accounting and performance ratios from the company's FY2024 financial statements (fiscal year ended December 31, 2024), benchmarked against FY2023 where applicable. The model enables management to assess Caterpillar's financial health, operational efficiency, capital structure leverage, and long-term value creation. Outputs are intended to support a CFO briefing and investor relations review, with Stage 4 feeding directly into an executive interpretation memo.

---

## 2. Inputs (Known Variables)

All figures in millions of USD unless otherwise noted.

### Balance Sheet Items (Current Year and Prior Year)

| Variable | Description | Named Range | FY2024 | FY2023 |
|---|---|---|---:|---:|
| Cash & marketable securities | Liquid assets | `BAL_cash_marketable_securities_[year]` | 5,728 | 6,061 |
| Receivables | Accounts receivable | `BAL_receivables_[year]` | 8,142 | 8,014 |
| Inventories | Inventory balance | `BAL_inventories_[year]` | 12,476 | 13,693 |
| Total current assets | Sum of current assets | `BAL_assets_current_[year]` | 28,201 | 29,488 |
| Net tangible fixed assets | PP&E less accumulated depreciation | `BAL_fixed_assets_net_[year]` | 6,167 | 6,079 |
| Total assets | All assets | `BAL_assets_total_[year]` | 86,028 | 82,432 |
| Total current liabilities | Short-term obligations | `BAL_liabilities_current_[year]` | 20,075 | 19,679 |
| Long-term debt | Non-current borrowings | `BAL_debt_long_term_[year]` | 25,046 | 25,107 |
| Total liabilities | All liabilities | `BAL_liabilities_total_[year]` | 53,847 | 53,470 |
| Shareholders' equity | Book value of equity | `BAL_equity_shareholders_[year]` | 32,181 | 28,962 |

### Income Statement Items

| Variable | Description | Named Range | FY2024 |
|---|---|---|---:|
| Net sales | Total revenue | `INC_sales` | 64,809 |
| Cost of goods sold | Direct production costs | `INC_cost_goods_sold` | 43,244 |
| SG&A expenses | Selling, general & administrative | `INC_sga` | 21,565 * |
| Depreciation | Non-cash charge | `INC_depreciation` | 1,413 |
| EBIT | Earnings before interest & taxes | `INC_ebit` | 14,187 |
| Other income | Non-operating income | `INC_other_income` | 2,116 |
| Interest expense | Cost of debt | `INC_interest_expense` | 1,713 |
| Taxes | Income tax expense | `INC_taxes` | 2,944 |
| Net income | Bottom-line earnings | `INC_net` | 5,262 |
| Dividends | Shareholder distributions | `INC_dividends` | 2,736 |

*\*See Model Review — SG&A appears to reflect gross profit rather than a separately sourced operating expense line.*

### Cash Flow Statement Items

| Variable | Description | Named Range | FY2024 |
|---|---|---|---:|
| Cash from operations | Operating cash flow | `CASH_operating` | 13,720 |
| Cash from investments | Investing cash flow | `CASH_investments` | (2,186) |

### Market / Analyst Inputs

| Variable | Description | Named Range | Value |
|---|---|---|---|
| Share price | Fiscal year-end closing price | `share_price` | $349.58 |
| Shares outstanding | Total shares (millions) | `shares_outstanding` | 492M |
| Cost of capital | Estimated WACC | `cost_capital` | 7.9% |
| Tax rate | Analyst assumption | `tax_rate` | 21.4% |

---

## 3. Assumptions & Constraints

- All figures reported in millions of USD unless otherwise noted.
- Tax rate set at 21.4% as a standard analyst assumption; the effective tax rate from the 10-K filing may differ and should be cross-referenced in a refined model.
- Cost of capital estimated at 7.9% (WACC approximation); this figure may be refined using CAPM with observed beta and current risk-free rate.
- Share price reflects the fiscal year-end closing price ($349.58) for CAT on December 31, 2024.
- Depreciation is sourced from the Income Statement and is consistent with the Cash Flow Statement add-back.
- Start-of-year values use the FY2023 Balance Sheet; current-year values use the FY2024 Balance Sheet.
- No off-balance-sheet items, operating lease obligations (ASC 842), or contingent liabilities are incorporated.
- Interest expense and revenue are treated on a simple annual basis.
- Market capitalization is computed as share price × shares outstanding (fully diluted shares not applied).

---

## 4. Calculation Flow

All formulas use named-range pseudocode. Values below reflect the corrected, intended outputs — see Section 7 for notes on Stage 2 discrepancies.

### Step 1: Derived Inputs

1. `market_capitalization` = `share_price` × `shares_outstanding` = **$171,993M**
2. `currentYear_after_tax_operating_income` = `INC_net` + (1 − `tax_rate`) × `INC_interest_expense` = **$6,608M**
3. `currentYear_daily_sales_average` = `INC_sales` / 365 = **$177.56M/day**
4. `currentYear_cost_goods_sold_daily` = `INC_cost_goods_sold` / 365 = **$118.48M/day**
5. `startYear_total_capitalization` = `BAL_debt_long_term_2023` + `BAL_equity_shareholders_2023` = **$54,069M**
6. `currentYear_total_capitalization` = `BAL_debt_long_term_2024` + `BAL_equity_shareholders_2024` = **$57,227M**
7. `currentYear_working_capital_net` = `BAL_assets_current_2024` − `BAL_liabilities_current_2024` = **$8,126M**
8. `avg_equity` = AVERAGE(`startYear_equity`, `currentYear_equity`) = **$30,571.5M**
9. `avg_total_assets` = AVERAGE(`startYear_total_assets`, `currentYear_assets_total`) = **$84,230M**
10. `avg_total_capitalization` = AVERAGE(`startYear_total_capitalization`, `currentYear_total_capitalization`) = **$55,648M**

### Step 2: Performance Ratios

| Ratio | Named-Range Formula | Corrected Value |
|---|---|---|
| Market Value Added (MVA) | `market_capitalization` − `currentYear_equity` | $139,812M |
| Market-to-Book | `market_capitalization` / `currentYear_equity` | 5.34× |
| Economic Value Added (EVA) | `currentYear_after_tax_operating_income` − (`cost_capital` × `startYear_total_capitalization`) | $2,337M |

### Step 3: Profitability Ratios

| Ratio | Named-Range Formula | Corrected Value |
|---|---|---|
| ROA | `currentYear_after_tax_operating_income` / `startYear_total_assets` | 8.02% |
| ROC | `currentYear_after_tax_operating_income` / `startYear_total_capitalization` | 12.22% |
| ROE | `INC_net` / `startYear_equity` | 18.16% |
| ROA [avg] | `currentYear_after_tax_operating_income` / `avg_total_assets` | 7.85% |
| ROC [avg] | `currentYear_after_tax_operating_income` / `avg_total_capitalization` | 11.87% |
| ROE [avg] | `INC_net` / `avg_equity` | 17.21% |

### Step 4: Efficiency Ratios

| Ratio | Named-Range Formula | Corrected Value |
|---|---|---|
| Asset Turnover | `INC_sales` / `startYear_total_assets` | 0.79× |
| Receivables Turnover | `INC_sales` / `startYear_receivables` | 8.09× |
| Avg Collection Period (days) | `startYear_receivables` / `currentYear_daily_sales_average` | 45.1 days |
| Inventory Turnover | `INC_cost_goods_sold` / `startYear_inventory` | 3.16× |
| Days in Inventory | `startYear_inventory` / `currentYear_cost_goods_sold_daily` | 115.6 days |
| Profit Margin | `INC_net` / `INC_sales` | 8.12% |
| Operating Profit Margin | `currentYear_after_tax_operating_income` / `INC_sales` | 10.20% |

### Step 5: Leverage Ratios

| Ratio | Named-Range Formula | Corrected Value |
|---|---|---|
| Long-term Debt Ratio | `currentYear_debt_long_term` / (`currentYear_debt_long_term` + `currentYear_equity`) | 43.8% |
| Long-term Debt-Equity Ratio | `currentYear_debt_long_term` / `currentYear_equity` | 0.78× |
| Total Debt Ratio | `currentYear_liabilities_total` / `currentYear_assets_total` | 62.6% |
| Times Interest Earned | `INC_ebit` / `INC_interest_expense` | 8.28× |
| Cash Coverage Ratio | (`INC_ebit` + `INC_depreciation`) / `INC_interest_expense` | 9.11× |
| Debt Burden | `INC_net` / `currentYear_after_tax_operating_income` | 0.80 |
| Leverage Ratio | `currentYear_assets_total` / `currentYear_equity` | 2.67× |

### Step 6: Liquidity Ratios

| Ratio | Named-Range Formula | Corrected Value |
|---|---|---|
| NWC-to-Assets | `currentYear_working_capital_net` / `currentYear_assets_total` | 9.4% |
| Current Ratio | `currentYear_assets_current` / `currentYear_liabilities_current` | 1.41× |
| Quick Ratio | (`currentYear_cash_marketable_securities` + `BAL_receivables_2024`) / `currentYear_liabilities_current` | 0.69× |
| Cash Ratio | `currentYear_cash_marketable_securities` / `currentYear_liabilities_current` | 0.29× |

### Step 7: Du Pont Decomposition

**Du Pont ROA** = `RATIO_asset_turnover` × `RATIO_operating_profit_margin`
= 0.786 × 10.20% = **8.02%** *(reconciles to direct ROA)*

**Du Pont ROE** = `RATIO_leverage` × `RATIO_asset_turnover` × `RATIO_operating_profit_margin` × `RATIO_debt_burden`
= 2.67 × 0.786 × 10.20% × 0.80 = **17.11%** *(reconciles to direct ROE within rounding)*

---

## 5. Outputs

| Output | Description | Format | Purpose |
|---|---|---|---|
| Ratio summary table | 25+ ratios organized by category | Table | Core analytical deliverable |
| Du Pont decomposition | ROA and ROE broken into component drivers | Table | Identifies levers of return |
| Named-range formula column | Pseudocode for each ratio | Column | Auditability and reproducibility |
| Reconciliation checks | Du Pont vs. direct ROA/ROE comparison | Inline | Formula validation |
| Executive summary | Key findings and strategic recommendations | 1–2 paragraphs | Stage 4 AI prompt input |

---

## 7. Model Review — What Worked & What to Improve

**What worked well:**
- The Balance Sheet and Cash Flow Statement tabs are cleanly structured and accurately sourced from the CAT FY2024 10-K. The balance check (Total Assets − Total Liabilities & Equity = 0) is correctly implemented, confirming data integrity.
- Named range conventions are consistently established in the Ratios tab, making the model self-documenting and largely readable without external reference.
- Derived inputs — market capitalization, net working capital, daily sales and COGS averages, and start/current/average capitalization figures — are correctly computed and clearly labeled.
- The leverage and liquidity ratio sections (debt ratios, current, quick, cash, NWC-to-assets) are structurally correct and produce reasonable results.
- The Du Pont decomposition architecture is sound, with proper component linkages; errors in that section are inherited rather than structural.

**What needs to be corrected:**

1. **After-tax operating income formula was not applied.** The cell returns `INC_net` (5,262) rather than the correct `INC_net + (1 − tax_rate) × INC_interest_expense` ≈ $6,608M. This single error cascades into ROA, ROC, EVA, operating profit margin, and Du Pont ROA — all are understated as a result.

2. **ROE (start-of-year) references the wrong cell.** The output displays 82,432 — which is `startYear_total_assets` — rather than `INC_net / startYear_equity` = 18.16%. This also corrupted the debt burden ratio, whose numerator links to the ROE output cell, producing an inflated result of ~15.67 instead of the correct ~0.80.

3. **Times interest earned and cash coverage are near-zero (~0.000125× and ~0.000171×).** The `INC_ebit` named range appears to point to the `tax_rate` cell (0.214) rather than the EBIT value (14,187). The correct TIE is 8.28× and cash coverage is 9.11×. These are significant — a TIE of 8.28× signals adequate but not exceptional interest coverage, a material insight that was lost.

4. **Receivables and inventory turnover values appear mis-referenced.** Receivables turnover should be 8.09× (`INC_sales / startYear_receivables`); inventory turnover should be 3.16× (`INC_cost_goods_sold / startYear_inventory`). The values in the model do not match either the correct formula or its inverse.

5. **Profit margin shows ~40.75 rather than 8.12%.** The correct formula is `INC_net / INC_sales`. The source of the wrong output is unclear but likely involves referencing incorrect input cells.

6. **SG&A on the Income Statement equals gross profit ($21,565M = Net Sales − COGS).** This indicates SG&A was entered as a residual plug rather than sourced from the 10-K's operating expense footnotes. In a refined model, SG&A should be pulled directly from the financial statements.

7. **Net income on the Cash Flow Statement ($11,646M) does not reconcile to the Income Statement ($5,262M).** Both figures need to be verified against the CAT 10-K; one or both likely reference incorrect cells or values. The income statement net income of $5,262M also warrants verification, as the implied tax rate (taxes of $2,944M / taxable income of $5,262M = 56%) is inconsistent with the stated 21.4% assumption.

**What would improve auditability:**
- Implement a three-tier color-coding scheme: blue for hard-coded analyst assumptions, yellow for financial statement data inputs, and green for computed formula outputs.
- Add a reconciliation row beneath the Du Pont section comparing Du Pont ROA/ROE to direct calculations; a discrepancy flag greater than 0.1% should be highlighted red.
- Include a formula audit column showing named-range pseudocode adjacent to the Excel cell formula for every computed ratio.

**Additional analysis worth including:**
- Three-year trend analysis (FY2022–FY2024) to put current ratios in historical context.
- Industry peer comparison against Deere & Company (DE) and CNH Industrial for relative benchmarking of margins and turnover.
- Sensitivity table for EVA across WACC ± 1% to quantify how sensitive value creation is to cost of capital assumptions.

---

## 8. Limitations & Next Steps

This specification does not incorporate peer benchmarking, multi-year trend analysis, operating lease obligations (ASC 842), segment-level breakdowns, or off-balance-sheet items. Several ratio outputs in the Stage 2 model require formula correction before reliable management interpretation can be conducted.

The next phase (Stage 4) will involve writing a structured AI prompt using this specification's named ranges and corrected calculation flow to produce a polished, auditable model, followed by an executive memo interpreting the ratio results for the CFO. The corrected values documented in Section 4 above should serve as the verification benchmark for the Stage 4 output.
