# Caterpillar Inc. (CAT) FY2024 Ratio Analysis – Technical Specification

**Created by:** Caden Chew
**Updated by:** Caden Chew
**Date Created:** April 24, 2026
**Date Updated:** April 24, 2026
**Version:** 1.0
**LLM Used:** Claude (Anthropic)

**Role:** Financial Analyst / FP&A Analyst
**Audience:** CFO or Director of FP&A

**Purpose:** Document the analytical structure for computing 25+ accounting and performance ratios from Caterpillar Inc.'s FY2024 financial statements, and articulate a refined, improved version of the Stage 2 Excel model.

---

## 1. Problem Statement

Caterpillar Inc. (CAT) is a publicly traded Industrials company specializing in heavy machinery and equipment. This specification outlines the analytical framework for computing 25+ accounting and performance ratios from the company's FY2024 financial statements (fiscal year ended December 31, 2024), benchmarked against FY2023 where applicable. The objective is to assess Caterpillar's financial health, operational efficiency, capital structure, and long-term value creation — outputs intended to support a CFO briefing and investor relations review.

---

## 2. Inputs (Known Variables)

All figures in millions of USD unless otherwise noted.

### Balance Sheet Items (Current Year and Prior Year)

| Variable | Named Range | FY2024 | FY2023 |
|---|---|---:|---:|
| Cash & marketable securities | `BAL_cash_marketable_securities_[year]` | 5,728 | 6,061 |
| Receivables | `BAL_receivables_[year]` | 8,142 | 8,014 |
| Inventories | `BAL_inventories_[year]` | 12,476 | 13,693 |
| Total current assets | `BAL_assets_current_[year]` | 28,201 | 29,488 |
| Net tangible fixed assets | `BAL_fixed_assets_net_[year]` | 6,167 | 6,079 |
| Total assets | `BAL_assets_total_[year]` | 86,028 | 82,432 |
| Total current liabilities | `BAL_liabilities_current_[year]` | 20,075 | 19,679 |
| Long-term debt | `BAL_debt_long_term_[year]` | 25,046 | 25,107 |
| Total liabilities | `BAL_liabilities_total_[year]` | 53,847 | 53,470 |
| Shareholders' equity | `BAL_equity_shareholders_[year]` | 32,181 | 28,962 |

### Income Statement Items

| Variable | Named Range | FY2024 |
|---|---|---:|
| Net sales | `INC_sales` | 64,809 |
| Cost of goods sold | `INC_cost_goods_sold` | 43,244 |
| SG&A expenses | `INC_sga` | 21,565 |
| Depreciation | `INC_depreciation` | 1,413 |
| EBIT | `INC_ebit` | 14,187 |
| Other income | `INC_other_income` | 2,116 |
| Interest expense | `INC_interest_expense` | 1,713 |
| Taxes | `INC_taxes` | 2,944 |
| Net income | `INC_net` | 5,262 |
| Dividends | `INC_dividends` | 2,736 |

### Cash Flow Statement Items

| Variable | Named Range | FY2024 |
|---|---|---:|
| Cash from operations | `CASH_operating` | 13,720 |
| Cash from investments | `CASH_investments` | (2,186) |

### Market / Analyst Inputs

| Variable | Named Range | Value |
|---|---|---|
| Share price (fiscal year-end) | `share_price` | $349.58 |
| Shares outstanding | `shares_outstanding` | 492M |
| Cost of capital (WACC est.) | `cost_capital` | 7.9% |
| Tax rate (analyst assumption) | `tax_rate` | 21.4% |

---

## 3. Named Range Conventions

All named ranges follow a standardized prefix structure so they are unambiguous in formulas and AI prompts. Balance Sheet items are prefixed `BAL_` with a year suffix (e.g., `BAL_equity_shareholders_2024`). Income Statement items are prefixed `INC_` with no year suffix since only FY2024 data is used (e.g., `INC_ebit`). Cash flow items use `CASH_`. Analyst assumptions use lowercase with no prefix (e.g., `cost_capital`, `tax_rate`). Derived intermediaries use a descriptive camelCase convention (e.g., `currentYear_after_tax_operating_income`, `avg_equity`). Ratio outputs are prefixed `RATIO_` where they are consumed by the Du Pont decomposition (e.g., `RATIO_asset_turnover`, `RATIO_leverage`).

---

## 4. Assumptions & Constraints

- All figures in millions of USD unless otherwise noted.
- Tax rate fixed at 21.4% as analyst assumption; effective rate from the 10-K may differ.
- Cost of capital estimated at 7.9% (WACC approximation); may be refined via CAPM.
- Share price reflects the fiscal year-end closing price as of December 31, 2024.
- Depreciation sourced from the Income Statement, consistent with the Cash Flow Statement add-back.
- Start-of-year values use the FY2023 Balance Sheet; current-year values use FY2024.
- No off-balance-sheet items, operating lease obligations (ASC 842), or contingent liabilities included.
- Market capitalization computed as `share_price` × `shares_outstanding`; fully diluted shares not applied.

---

## 5. Calculation Flow

### Step 1: Derived Inputs
1. `market_capitalization` = `share_price` × `shares_outstanding`
2. `currentYear_after_tax_operating_income` = `INC_net` + (1 − `tax_rate`) × `INC_interest_expense`
3. `currentYear_daily_sales_average` = `INC_sales` / 365
4. `currentYear_cost_goods_sold_daily` = `INC_cost_goods_sold` / 365
5. `startYear_total_capitalization` = `BAL_debt_long_term_2023` + `BAL_equity_shareholders_2023`
6. `currentYear_total_capitalization` = `BAL_debt_long_term_2024` + `BAL_equity_shareholders_2024`
7. `currentYear_working_capital_net` = `BAL_assets_current_2024` − `BAL_liabilities_current_2024`
8. `avg_equity` = AVERAGE(`BAL_equity_shareholders_2023`, `BAL_equity_shareholders_2024`)
9. `avg_total_assets` = AVERAGE(`BAL_assets_total_2023`, `BAL_assets_total_2024`)
10. `avg_total_capitalization` = AVERAGE(`startYear_total_capitalization`, `currentYear_total_capitalization`)

### Step 2: Performance Ratios
- MVA = `market_capitalization` − `BAL_equity_shareholders_2024`
- Market-to-Book = `market_capitalization` / `BAL_equity_shareholders_2024`
- EVA = `currentYear_after_tax_operating_income` − (`cost_capital` × `startYear_total_capitalization`)

### Step 3: Profitability Ratios
- ROA = `currentYear_after_tax_operating_income` / `BAL_assets_total_2023`
- ROC = `currentYear_after_tax_operating_income` / `startYear_total_capitalization`
- ROE = `INC_net` / `BAL_equity_shareholders_2023`
- ROA [avg] = `currentYear_after_tax_operating_income` / `avg_total_assets`
- ROC [avg] = `currentYear_after_tax_operating_income` / `avg_total_capitalization`
- ROE [avg] = `INC_net` / `avg_equity`

### Step 4: Efficiency Ratios
- Asset Turnover = `INC_sales` / `BAL_assets_total_2023`
- Receivables Turnover = `INC_sales` / `BAL_receivables_2023`
- Avg Collection Period = `BAL_receivables_2023` / `currentYear_daily_sales_average`
- Inventory Turnover = `INC_cost_goods_sold` / `BAL_inventories_2023`
- Days in Inventory = `BAL_inventories_2023` / `currentYear_cost_goods_sold_daily`
- Profit Margin = `INC_net` / `INC_sales`
- Operating Profit Margin = `currentYear_after_tax_operating_income` / `INC_sales`

### Step 5: Leverage Ratios
- Long-term Debt Ratio = `BAL_debt_long_term_2024` / (`BAL_debt_long_term_2024` + `BAL_equity_shareholders_2024`)
- Long-term Debt-Equity Ratio = `BAL_debt_long_term_2024` / `BAL_equity_shareholders_2024`
- Total Debt Ratio = `BAL_liabilities_total_2024` / `BAL_assets_total_2024`
- Times Interest Earned = `INC_ebit` / `INC_interest_expense`
- Cash Coverage = (`INC_ebit` + `INC_depreciation`) / `INC_interest_expense`
- Debt Burden = `INC_net` / `currentYear_after_tax_operating_income`
- Leverage Ratio = `BAL_assets_total_2024` / `BAL_equity_shareholders_2024`

### Step 6: Liquidity Ratios
- NWC-to-Assets = `currentYear_working_capital_net` / `BAL_assets_total_2024`
- Current Ratio = `BAL_assets_current_2024` / `BAL_liabilities_current_2024`
- Quick Ratio = (`BAL_cash_marketable_securities_2024` + `BAL_receivables_2024`) / `BAL_liabilities_current_2024`
- Cash Ratio = `BAL_cash_marketable_securities_2024` / `BAL_liabilities_current_2024`

### Step 7: Du Pont Decomposition
- Du Pont ROA = `RATIO_asset_turnover` × `RATIO_operating_profit_margin`
- Du Pont ROE = `RATIO_leverage` × `RATIO_asset_turnover` × `RATIO_operating_profit_margin` × `RATIO_debt_burden`

---

## 6. Outputs

| Output | Description | Format | Purpose |
|---|---|---|---|
| Ratio summary table | All 25+ ratios grouped by category: Performance, Profitability, Efficiency, Leverage, Liquidity | Table | Core analytical deliverable |
| Du Pont decomposition table | ROA and ROE broken into Asset Turnover, Operating Margin, Leverage, and Debt Burden with component linkages displayed | Table | Identifies specific drivers of return |
| Derived inputs summary | Computed intermediaries: market cap, after-tax operating income, daily averages, and capitalization totals | Table | Transparency and auditability |
| Named-range formula column | Pseudocode formula displayed alongside each computed ratio | Inline column | Allows any analyst to verify logic without opening the formula bar |
| Du Pont reconciliation check | Direct ROA/ROE compared to Du Pont component product; flags discrepancies exceeding 0.1% | Inline row | Built-in formula validation |
| Executive summary | 1–2 paragraph narrative of key findings and strategic recommendations | Prose | Direct input for Stage 4 CFO memo |

---

## 7. Model Review — What Worked & What to Improve

**What worked well:** The Balance Sheet and Cash Flow tabs are accurately sourced from the CAT FY2024 10-K — the balance check (Total Assets − Total Liabilities & Equity = 0) confirms data integrity. Named range conventions are consistently applied across the Ratios tab, making the model largely self-documenting. Derived inputs — market cap, net working capital, daily averages, and capitalization figures — are correctly computed and clearly labeled. The leverage and liquidity sections produce structurally correct outputs, and the Du Pont architecture correctly links to its component ratios.

**What needs improvement:** Several formula errors cascade into material misstatements. `currentYear_after_tax_operating_income` returns `INC_net` unchanged — the after-tax interest add-back was not applied — which understates ROA, ROC, EVA, and operating margin throughout. The start-of-year ROE cell references `BAL_assets_total_2023` rather than `INC_net` / `BAL_equity_shareholders_2023`, which also inflates the debt burden ratio linked to it. `INC_ebit` appears to reference the `tax_rate` cell rather than the EBIT value, producing near-zero outputs for Times Interest Earned and Cash Coverage — two of the more decision-relevant ratios for assessing debt serviceability. Finally, the SG&A entry on the Income Statement appears to be a residual plug (Net Sales − COGS) rather than an independently sourced figure from the 10-K; this should be corrected in the refined model.

**What would make the model more auditable:** Consistent color-coding — blue for analyst assumptions, yellow for financial statement inputs, green for computed outputs — would reduce review time. The Du Pont reconciliation check described in Section 6 should be treated as a standard build requirement. A formula audit column displaying named-range pseudocode next to every live formula would allow any reviewer to verify logic at a glance.

**Additional analysis worth including:** A three-year trend panel (FY2022–FY2024) to contextualize ratios historically, and a peer comparison against Deere & Company and CNH Industrial to benchmark Caterpillar's margins, turnover, and leverage within the heavy machinery sector.

---

## 8. Limitations & Next Steps

This model does not incorporate peer benchmarking, multi-year trend analysis, operating lease obligations (ASC 842), or segment-level breakdowns. Several ratio outputs require formula correction before reliable management interpretation is possible.

The Stage 4 AI prompt will draw directly from the named ranges and calculation flow in Section 5 to produce a corrected, auditable model. The executive memo will then interpret the verified ratio outputs for the CFO, with emphasis on Caterpillar's capital efficiency, leverage profile, and value creation relative to cost of capital.
