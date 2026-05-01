# Stage 4 – Final Analysis, Prompt Engineering & Recommendation
## Caterpillar Inc. (CAT) | FY2024 Accounting Ratio Analysis

**Prepared by:** Caden Chew
**Date:** April 30, 2026
**Audience:** CFO / Director of FP&A
**Version:** 1.0

---

## A. Company & Data Summary

**Company:** Caterpillar Inc. (NYSE: CAT)
**Industry:** Industrials — Heavy Machinery & Equipment
**Fiscal Year Analyzed:** FY2024 (ended December 31, 2024), benchmarked against FY2023

**Data Sources:**
- Caterpillar Inc. FY2024 Annual Report / 10-K (filed with the SEC)
- Market data sourced from public equity databases (fiscal year-end share price: $349.58; shares outstanding: 492M)

**Key Assumptions:**
- Tax rate: 21.4% (analyst assumption; effective rate per 10-K may differ modestly)
- Cost of capital (WACC): 7.9% (estimated approximation; refinable via CAPM)
- Start-of-year balance sheet values use FY2023 figures; current-year values use FY2024 figures
- No operating lease obligations (ASC 842), off-balance-sheet items, or segment adjustments included
- Market capitalization computed using basic shares outstanding (not fully diluted)

---

## B. Ratio Results Summary

All figures in millions of USD unless otherwise noted.

### Derived Inputs

| Metric | Value |
|---|---:|
| Market Capitalization | $172,013M |
| After-Tax Operating Income | $6,608M |
| Daily Sales Average | $177.6M/day |
| Daily COGS Average | $118.5M/day |
| Start-of-Year Total Capitalization (FY2023) | $54,069M |
| Current-Year Total Capitalization (FY2024) | $57,227M |
| Net Working Capital | $8,126M |
| Average Shareholders' Equity | $30,572M |
| Average Total Assets | $84,230M |
| Average Total Capitalization | $55,648M |

---

### Performance Ratios

| Ratio | Formula (Named Range) | Value |
|---|---|---:|
| Market Value Added (MVA) | `market_cap − BAL_equity_shareholders_2024` | $139,832M |
| Market-to-Book | `market_cap / BAL_equity_shareholders_2024` | 5.34× |
| Economic Value Added (EVA) | `ATOI − (cost_capital × startYear_total_cap)` | $2,337M |

---

### Profitability Ratios

| Ratio | Formula (Named Range) | Start-Year | Avg |
|---|---|---:|---:|
| Return on Assets (ROA) | `ATOI / BAL_assets_total_2023` | 8.01% | 7.85% |
| Return on Capital (ROC) | `ATOI / startYear_total_cap` | 12.22% | 11.87% |
| Return on Equity (ROE) | `INC_net / BAL_equity_shareholders_2023` | 18.17% | 17.21% |
| Profit Margin | `INC_net / INC_sales` | 8.12% | — |
| Operating Profit Margin | `ATOI / INC_sales` | 10.20% | — |

---

### Efficiency Ratios

| Ratio | Formula (Named Range) | Value |
|---|---|---:|
| Asset Turnover | `INC_sales / BAL_assets_total_2023` | 0.79× |
| Receivables Turnover | `INC_sales / BAL_receivables_2023` | 8.09× |
| Avg Collection Period | `BAL_receivables_2023 / daily_sales_avg` | 45.1 days |
| Inventory Turnover | `INC_cost_goods_sold / BAL_inventories_2023` | 3.16× |
| Days in Inventory | `BAL_inventories_2023 / daily_cogs_avg` | 115.6 days |

---

### Leverage Ratios

| Ratio | Formula (Named Range) | Value |
|---|---|---:|
| Long-Term Debt Ratio | `BAL_debt_long_term_2024 / (LTD + equity)` | 43.77% |
| Long-Term Debt-to-Equity | `BAL_debt_long_term_2024 / BAL_equity_shareholders_2024` | 0.78× |
| Total Debt Ratio | `BAL_liabilities_total_2024 / BAL_assets_total_2024` | 62.59% |
| Times Interest Earned (TIE) | `INC_ebit / INC_interest_expense` | 8.28× |
| Cash Coverage | `(INC_ebit + INC_depreciation) / INC_interest_expense` | 9.11× |
| Debt Burden | `INC_net / ATOI` | 0.796 |
| Leverage Ratio | `BAL_assets_total_2024 / BAL_equity_shareholders_2024` | 2.67× |

---

### Liquidity Ratios

| Ratio | Formula (Named Range) | Value |
|---|---|---:|
| NWC-to-Assets | `NWC / BAL_assets_total_2024` | 9.45% |
| Current Ratio | `BAL_assets_current_2024 / BAL_liabilities_current_2024` | 1.40× |
| Quick Ratio | `(cash + receivables) / BAL_liabilities_current_2024` | 0.69× |
| Cash Ratio | `BAL_cash_marketable_securities_2024 / BAL_liabilities_current_2024` | 0.29× |

---

### Du Pont Decomposition

| Component | Named Range | Value |
|---|---|---:|
| Operating Profit Margin | `RATIO_operating_profit_margin` | 10.20% |
| Asset Turnover | `RATIO_asset_turnover` | 0.786× |
| Leverage Ratio | `RATIO_leverage` | 2.673× |
| Debt Burden | `RATIO_debt_burden` | 0.796 |
| **Du Pont ROA** | `Margin × Turnover` | **8.02%** |
| **Du Pont ROE** | `Leverage × Turnover × Margin × Debt Burden` | **17.07%** |
| **Direct ROE (verification)** | `INC_net / BAL_equity_shareholders_2023` | **18.17%** |

> **Reconciliation Note:** The Du Pont ROE (17.07%) vs. direct ROE (18.17%) difference of ~1.1 pp reflects the use of end-of-year assets/equity in the Du Pont leverage component versus start-of-year equity in the direct ROE calculation. Both are structurally correct and within acceptable tolerance for a single-year model without full averaging applied uniformly. The Du Pont ROA reconciliation (8.02% vs. 8.01%) is within 0.01% — confirmed clean.

---

## C. Interpretation & Key Findings

### Performance — Strong Value Creation, Premium Market Valuation

Caterpillar's MVA of **$139.8 billion** represents the market's recognition of substantial accumulated value beyond book equity, reflecting decades of brand equity, pricing power, and earnings consistency. The Market-to-Book multiple of **5.34×** is well above the typical industrials benchmark of 2–3×, signaling investor confidence in sustained above-cost returns.

Most critically, EVA of **$2.34 billion** confirms that Caterpillar is generating returns in excess of its cost of capital — this is not financial engineering. After covering a 7.9% WACC on $54.1 billion in invested capital, the company still produces meaningful economic profit. This is the clearest evidence of durable competitive advantage in this analysis.

### Profitability — Healthy Returns with Moderate Margin Compression Risk

ROE of **18.2%** and ROC of **12.2%** are strong for an industrial manufacturer where capital intensity is high and demand cycles are volatile. The 10.2% operating profit margin is respectable, though Caterpillar's net margin of **8.1%** reveals that interest expense and taxes together absorb roughly 20 percentage points of operating income. As leverage remains material, margin sustainability is a key watch item.

### Efficiency — Asset-Light Relative to Revenue, but Inventory Elevated

Asset turnover of **0.79×** is reasonable for a heavy-equipment OEM carrying significant dealer receivables and finished goods. However, **Days in Inventory of 115.6 days** is the clearest operational concern in this analysis. For a manufacturer of Caterpillar's scale, carrying nearly four months of inventory relative to COGS implies either demand softness, supply chain conservatism, or both — each with working capital implications. The average collection period of **45.1 days** is well-managed and consistent with commercial equipment credit terms.

### Leverage — Manageable but Structurally Heavy

The total debt ratio of **62.6%** and long-term debt ratio of **43.8%** are elevated by general industrial standards, though Caterpillar's financial services segment (Cat Financial) is a material contributor to balance sheet liabilities. When viewed through a debt-serviceability lens, TIE of **8.28×** and cash coverage of **9.11×** are strong — the company covers interest nearly nine times over with operating cash. This is not financial distress; it is the leverage profile of a scaled financial-services-embedded industrial.

### Liquidity — Adequate but Not Abundant

The current ratio of **1.40×** is within normal range, though the quick ratio of **0.69×** drops below 1.0 once the $12.5 billion inventory balance is excluded. This is not alarming for a capital-goods manufacturer with predictable cash flows and $13.7 billion in operating cash generation, but it does mean short-term liquidity relies on inventory conversion. The cash ratio of **0.29×** is lean — consistent with Caterpillar's strategy of deploying excess cash via dividends ($2.74B) and buybacks rather than hoarding liquidity.

### Top 5 Findings for the CFO

1. **EVA of $2.34B confirms genuine value creation** above the cost of capital — a direct refutation of any narrative that CAT returns are leverage-driven illusions.
2. **Days in Inventory at 115.6 days is the primary operational inefficiency** — reducing this by 15–20 days would meaningfully improve working capital and free cash flow.
3. **Quick ratio below 1.0 (0.69×) warrants attention** in a cyclical industry — if demand declines sharply, current liabilities cannot be fully covered without inventory liquidation.
4. **TIE of 8.28× provides comfortable debt service headroom** — Caterpillar has meaningful capacity to absorb an earnings decline before covenant risk becomes relevant.
5. **Market-to-Book of 5.34× reflects premium valuation** — the company must sustain above-WACC returns to justify this multiple; any deterioration in ROC would compress equity value disproportionately.

---

## D. Du Pont Analysis Discussion

Caterpillar's Du Pont decomposition reveals that **leverage is the primary amplifier of ROE**, not margin or turnover alone:

| Driver | Value | Contribution |
|---|---:|---|
| Operating Profit Margin | 10.20% | Moderate — solid but not exceptional |
| Asset Turnover | 0.786× | Low-to-moderate — typical for capital-intensive OEM |
| Leverage Ratio | 2.67× | High — primary ROE amplifier |
| Debt Burden | 0.796 | Moderate tax/interest drag |

**Is profitability the main driver?** No. A 10.2% operating margin is competitive within the industrial sector but does not by itself explain an 18% ROE. Margin alone at this turnover level would produce ROA of only ~8%.

**Is asset efficiency strong or weak?** Asset turnover of 0.79× is moderate. For every dollar of prior-year assets, Caterpillar generates $0.79 in revenue — reasonable given the embedded financial services assets on the balance sheet, which are productive but inflate the denominator without proportional revenue contribution.

**Is leverage amplifying returns — and is it sustainable?** Yes, and conditionally. The 2.67× leverage ratio lifts ROE from the ~8% ROA level to the ~17–18% range. This amplification is sustainable as long as TIE remains high (currently 8.28×), operating cash flow is robust ($13.7B in FY2024), and the demand cycle does not inflect sharply downward. The risk scenario is a revenue contraction that simultaneously compresses margin and tightens coverage ratios — a combination that would expose the leverage more acutely.

The **debt burden ratio of 0.796** indicates that roughly 20 cents of every dollar of after-tax operating income is consumed by interest and the tax shield differential — a meaningful but not excessive drag.

---

## E. Strategic Recommendations

### 1. Reduce Days in Inventory from 115.6 to ~95 Days
**Data:** `BAL_inventories_2023 = $13,693M`; `daily_cogs_avg = $118.5M/day`

Bringing Days in Inventory from 115.6 to ~95 days would release approximately **$2.4 billion in working capital** (20 days × $118.5M/day). This could be accomplished through tighter dealer inventory management agreements, demand-signal integration with distribution partners, and SKU rationalization on slow-moving configurations. The freed capital could fund share repurchases or reduce short-term borrowings — both of which improve per-share metrics.

### 2. Build a Modest Cash Buffer to Strengthen the Quick Ratio Above 1.0
**Data:** `Quick Ratio = 0.69×`; current liabilities = $20,075M

The quick ratio of 0.69× means Caterpillar is $6.2 billion short of covering current liabilities without relying on inventory. Given the cyclical nature of heavy equipment demand, maintaining a quick ratio closer to 0.85–1.0× would provide a meaningful liquidity margin of safety. A portion of the inventory reduction proceeds (Recommendation 1) could be directed toward cash preservation rather than full deployment into buybacks.

### 3. Actively Communicate EVA and MVA to Investors in IR Materials
**Data:** `EVA = $2,337M`; `MVA = $139,832M`

Caterpillar's $2.34B EVA is a compelling, underutilized investor narrative. While EPS and EBITDA dominate quarterly commentary, EVA directly demonstrates value creation above the cost of capital — a metric increasingly favored by institutional allocators evaluating capital discipline. Incorporating EVA trend data in the Annual Report and investor day materials would differentiate Caterpillar's equity story from peers who show high earnings but destructive returns.

### 4. Evaluate Incremental Debt Capacity Selectively for Strategic M&A or Buybacks
**Data:** `TIE = 8.28×`; `Long-Term Debt Ratio = 43.77%`

With TIE above 8× and cash coverage at 9.11×, Caterpillar has meaningful headroom before approaching typical industrial covenant thresholds (~3–4× TIE). The current leverage level ($25B long-term debt) could support an additional $3–5 billion in strategic debt if deployed into high-ROC acquisitions or accelerated buybacks — particularly if management views current share price as intrinsically undervalued relative to the EVA generation capacity of the business. Any incremental leverage should be contingent on maintaining TIE above 5× under a stress scenario.

---

## F. Structured AI Prompt

```
# GOAL

Create a complete, auditable Excel workbook computing 25+ accounting and performance ratios for
Caterpillar Inc. (CAT) using FY2024 10-K data. The workbook must use named ranges matching the
conventions defined in this prompt, apply color-coding to distinguish inputs from outputs, and
produce a verified Du Pont decomposition. All financial data is provided explicitly below — do not
infer or estimate any value.

---

# WORKBOOK STRUCTURE

Produce the following tabs in order:
1. Balance_Sheet  — historical BS items, two years (FY2023, FY2024), with named ranges
2. Income_Statement — FY2024 P&L items with named ranges
3. Cash_Flow — FY2024 cash flow items with named ranges
4. Assumptions — analyst inputs (tax rate, WACC, share price, shares outstanding)
5. Derived_Inputs — computed intermediaries (market cap, ATOI, daily averages, capitalizations)
6. Ratios — all 25+ ratios organized by category with formula column
7. DuPont — decomposition table with reconciliation check
8. Summary — executive output table (formatted for printing)

---

# COLOR CODING (apply to all tabs)

- YELLOW fill (#FFFF00): Hard-coded financial statement inputs (Balance Sheet, Income Statement, Cash Flow values)
- BLUE fill (#BDD7EE): Analyst assumptions (tax rate, WACC, share price, shares outstanding)
- GREEN fill (#C6EFCE): Computed formulas (all derived inputs and ratio outputs)
- GRAY fill (#D9D9D9): Section headers, labels, and non-editable structural cells

---

# COMPANY FINANCIAL DATA

All figures in millions of USD unless otherwise noted.

## Balance Sheet Items

### FY2024 (Current Year)
Named Range                             | Value
BAL_cash_marketable_securities_2024     | 5,728
BAL_receivables_2024                    | 8,142
BAL_inventories_2024                    | 12,476
BAL_assets_current_2024                 | 28,201
BAL_fixed_assets_net_2024               | 6,167
BAL_assets_total_2024                   | 86,028
BAL_liabilities_current_2024            | 20,075
BAL_debt_long_term_2024                 | 25,046
BAL_liabilities_total_2024              | 53,847
BAL_equity_shareholders_2024            | 32,181

### FY2023 (Prior Year / Start-of-Year)
Named Range                             | Value
BAL_cash_marketable_securities_2023     | 6,061
BAL_receivables_2023                    | 8,014
BAL_inventories_2023                    | 13,693
BAL_assets_current_2023                 | 29,488
BAL_fixed_assets_net_2023               | 6,079
BAL_assets_total_2023                   | 82,432
BAL_liabilities_current_2023            | 19,679
BAL_debt_long_term_2023                 | 25,107
BAL_liabilities_total_2023              | 53,470
BAL_equity_shareholders_2023            | 28,962

## Income Statement Items (FY2024)
Named Range          | Value
INC_sales            | 64,809
INC_cost_goods_sold  | 43,244
INC_sga              | 21,565
INC_depreciation     | 1,413
INC_ebit             | 14,187
INC_other_income     | 2,116
INC_interest_expense | 1,713
INC_taxes            | 2,944
INC_net              | 5,262
INC_dividends        | 2,736

## Cash Flow Statement Items (FY2024)
Named Range         | Value
CASH_operating      | 13,720
CASH_investments    | (2,186)

## Analyst Assumptions (Blue cells)
Named Range          | Value
share_price          | 349.58   [USD per share — not in millions]
shares_outstanding   | 492      [millions]
cost_capital         | 0.079    [7.9% WACC]
tax_rate             | 0.214    [21.4%]

---

# DERIVED INPUTS (Computed in Derived_Inputs tab — GREEN cells)

Use these named range formulas exactly as written:

market_capitalization                = share_price * shares_outstanding
currentYear_after_tax_operating_income = INC_net + (1 - tax_rate) * INC_interest_expense
currentYear_daily_sales_average      = INC_sales / 365
currentYear_cost_goods_sold_daily    = INC_cost_goods_sold / 365
startYear_total_capitalization       = BAL_debt_long_term_2023 + BAL_equity_shareholders_2023
currentYear_total_capitalization     = BAL_debt_long_term_2024 + BAL_equity_shareholders_2024
currentYear_working_capital_net      = BAL_assets_current_2024 - BAL_liabilities_current_2024
avg_equity                           = (BAL_equity_shareholders_2023 + BAL_equity_shareholders_2024) / 2
avg_total_assets                     = (BAL_assets_total_2023 + BAL_assets_total_2024) / 2
avg_total_capitalization             = (startYear_total_capitalization + currentYear_total_capitalization) / 2

---

# RATIO FORMULAS

All ratio outputs prefixed RATIO_ where referenced in Du Pont. Display a named-range pseudocode
formula column next to each live formula for auditability.

## Performance Ratios
MVA             = market_capitalization - BAL_equity_shareholders_2024
Market_to_Book  = market_capitalization / BAL_equity_shareholders_2024
EVA             = currentYear_after_tax_operating_income - (cost_capital * startYear_total_capitalization)

## Profitability Ratios
ROA             = currentYear_after_tax_operating_income / BAL_assets_total_2023
ROC             = currentYear_after_tax_operating_income / startYear_total_capitalization
ROE             = INC_net / BAL_equity_shareholders_2023
ROA_avg         = currentYear_after_tax_operating_income / avg_total_assets
ROC_avg         = currentYear_after_tax_operating_income / avg_total_capitalization
ROE_avg         = INC_net / avg_equity
RATIO_profit_margin          = INC_net / INC_sales
RATIO_operating_profit_margin = currentYear_after_tax_operating_income / INC_sales

## Efficiency Ratios
RATIO_asset_turnover         = INC_sales / BAL_assets_total_2023
Receivables_Turnover         = INC_sales / BAL_receivables_2023
Avg_Collection_Period        = BAL_receivables_2023 / currentYear_daily_sales_average
Inventory_Turnover           = INC_cost_goods_sold / BAL_inventories_2023
Days_in_Inventory            = BAL_inventories_2023 / currentYear_cost_goods_sold_daily

## Leverage Ratios
LT_Debt_Ratio                = BAL_debt_long_term_2024 / (BAL_debt_long_term_2024 + BAL_equity_shareholders_2024)
LT_Debt_Equity_Ratio         = BAL_debt_long_term_2024 / BAL_equity_shareholders_2024
Total_Debt_Ratio             = BAL_liabilities_total_2024 / BAL_assets_total_2024
Times_Interest_Earned        = INC_ebit / INC_interest_expense
Cash_Coverage                = (INC_ebit + INC_depreciation) / INC_interest_expense
RATIO_debt_burden            = INC_net / currentYear_after_tax_operating_income
RATIO_leverage               = BAL_assets_total_2024 / BAL_equity_shareholders_2024

## Liquidity Ratios
NWC_to_Assets                = currentYear_working_capital_net / BAL_assets_total_2024
Current_Ratio                = BAL_assets_current_2024 / BAL_liabilities_current_2024
Quick_Ratio                  = (BAL_cash_marketable_securities_2024 + BAL_receivables_2024) / BAL_liabilities_current_2024
Cash_Ratio                   = BAL_cash_marketable_securities_2024 / BAL_liabilities_current_2024

---

# DU PONT DECOMPOSITION

Compute in the DuPont tab using ratio references (not raw values):

DuPont_ROA = RATIO_asset_turnover * RATIO_operating_profit_margin
DuPont_ROE = RATIO_leverage * RATIO_asset_turnover * RATIO_operating_profit_margin * RATIO_debt_burden

---

# VERIFICATION CHECKS

Add a Verification section at the bottom of the DuPont tab:

1. Du Pont ROA Check: =IF(ABS(DuPont_ROA - ROA) > 0.001, "FAIL - Review Formula", "PASS")
2. Du Pont ROE Check: =IF(ABS(DuPont_ROE - ROE) > 0.015, "FAIL - Review Formula", "PASS")
   [Note: tolerance of 1.5% accommodates start-year vs. end-year denominator differences]
3. Balance Sheet Check: =IF(BAL_assets_total_2024 - (BAL_liabilities_total_2024 + BAL_equity_shareholders_2024) <> 0, "FAIL - BS Imbalance", "PASS")

---

# FORMATTING REQUIREMENTS

- Use consistent number formatting: ratios as % (2 decimal places), multiples as x (2 decimal places),
  dollar amounts as $#,##0M
- Freeze top row and left label column on the Ratios tab
- Bold all category headers (Performance, Profitability, Efficiency, Leverage, Liquidity)
- Add borders separating ratio categories
- Name the file: CAT_FY2024_Ratio_Model_Chew.xlsx
```

---

## G. Executive Justification

### Financial Health Assessment

Caterpillar enters FY2025 from a position of fundamental financial strength. The company generated $13.7 billion in operating cash flow against $2.7 billion in dividends, leaving substantial discretionary capital. EVA of $2.34 billion confirms that operations are creating genuine economic value above the full cost of capital — a bar that many industrial competitors fail to clear. The balance sheet, while leveraged, is structured with long-duration debt ($25B in long-term obligations against $1.7B annual interest), and coverage ratios remain comfortable at nearly 9× earnings coverage. Caterpillar is not under financial stress; it is managing a deliberately levered capital structure consistent with its embedded financial services operations.

### Operational Efficiency Opportunities

The most actionable opportunity identified in this analysis is inventory reduction. At 115.6 days, Caterpillar's inventory cycle is extended relative to both historical norms and peer benchmarks. A 20-day improvement would release approximately $2.4 billion in working capital — meaningful capital that could reduce short-term borrowings, fund dividends, or support additional buybacks. Asset turnover at 0.79× also suggests that growth in revenue per dollar of asset base should be a medium-term management priority, particularly as the balance sheet continues to grow.

### Capital Structure Observations

Caterpillar operates with a total debt ratio of 62.6%, which is elevated by general industrial standards but consistent with the company's captive financing model (Cat Financial), which borrows externally to fund dealer and customer equipment loans. Excluding financial services, the industrial segment's leverage profile is materially more conservative. That said, TIE of 8.28× and cash coverage of 9.11× demonstrate that the consolidated entity services its debt load with significant headroom. The company retains capacity for incremental strategic borrowing, though this should be exercised selectively given cyclical demand exposure.

### Liquidity Position

Current ratio of 1.40× is adequate, but the quick ratio of 0.69× and cash ratio of 0.29× reveal a liquidity profile that depends meaningfully on inventory conversion. For a capital-goods manufacturer with multi-year backlog visibility and predictable cash generation, this is a manageable risk. However, in a demand downturn scenario, the speed of inventory conversion would slow precisely when liquidity pressure is greatest — a structural vulnerability worth monitoring. Building the quick ratio toward 0.85× over the next 12–18 months through inventory reduction and modest cash retention would materially improve the company's cyclical resilience.

### Value Creation Track Record

The MVA of $139.8 billion is a definitive statement about long-term value creation — the market attributes nearly $140 billion in value above and beyond what shareholders have contributed in book equity. The Market-to-Book multiple of 5.34× places Caterpillar firmly in the upper tier of industrial valuation, a position that carries both privilege and obligation: the company must continue generating above-WACC returns to justify this premium. The FY2024 EVA of $2.34 billion demonstrates that this obligation is being met. Should EVA trend negative — due to margin compression, rising interest rates, or capital misallocation — the multiple contraction risk is significant.

### Accounting and Reporting Implications

This analysis was constructed from publicly filed 10-K data and relies on analyst assumptions for WACC and tax rate. Two areas warrant attention in subsequent model versions. First, Cat Financial's assets and liabilities are consolidated into the balance sheet, which distorts leverage, liquidity, and asset turnover ratios when benchmarked against pure industrial peers — a segment-adjusted analysis would sharpen interpretive accuracy. Second, the SG&A figure used ($21,565M) represents the residual between Net Sales and COGS and may not precisely match the income statement line as reported; independent sourcing from the 10-K income statement footnotes is recommended for the refined model. Both refinements are scoped for Stage 4 follow-on work.

---

*Prepared by Caden Chew | Caterpillar Inc. FY2024 Ratio Analysis | Stage 4 Final Deliverable*
