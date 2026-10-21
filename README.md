# US Mortgage Affordability by State (2026)

Monthly mortgage payment for a median-value home in all 50 states and DC, as a share of median household income.

- Data: `calcwise-mortgage-affordability-by-state-2026.csv` (51 states/DC rows plus one United States row)
- Report and method: https://www.calcwise.tools/reports/mortgage-affordability-by-state
- License: CC BY 4.0 (the Census inputs are public domain)
- Version: 2026.1 (ACS 2024 1-year, rate week of Oct 15, 2026)

## Method

For each state: loan = 80% of median home value; principal and interest from the standard fixed-rate formula `M = P·r / (1 - (1+r)^-n)` at 7.40%, 30 years; plus median real estate taxes paid / 12. Share = payment / (median household income / 12). The range columns use every input at its 90% margin-of-error bound (value and tax minus MOE with income plus MOE for the low end, and the reverse for the high end). Insurance, PMI and HOA fees are not included.

## Columns

| Column | Meaning |
|---|---|
| rank_1_most_affordable | 1 = smallest payment share of income (empty for the US row) |
| state, abbr, fips | State name, USPS code, FIPS code (US row: 00) |
| median_home_value_usd / _moe90_usd | ACS B25077_001E and its 90% margin of error |
| median_property_tax_paid_usd / _moe90_usd | ACS B25103_001E, dollars per year |
| median_household_income_usd / _moe90_usd | ACS B19013_001E |
| down_payment_usd, loan_amount_usd | 20% of median value; remainder |
| mortgage_rate_pct | 7.4 (Freddie Mac PMMS 30-year, week of Oct 15, 2026) |
| monthly_principal_interest_usd | P&I on the loan |
| monthly_property_tax_usd | Annual tax / 12 |
| monthly_payment_usd | P&I + property tax |
| payment_share_of_gross_income_pct | Payment / gross monthly income |
| share_range_low_pct, share_range_high_pct | Range from the margins of error |
| income_needed_at_28pct_usd | Annual income at which the payment equals 28% |
| price_to_income_ratio | Median value / median household income |
| effective_property_tax_rate_pct | Median tax / median value |
| monthly_payment_at_year_ago_rate_usd, share_at_year_ago_rate_pct | Same calculation at 6.27% |

## Use it

```python
import pandas as pd
df = pd.read_csv("https://www.calcwise.tools/reports/mortgage-affordability-by-state/data.csv")
print(df.nlargest(5, "payment_share_of_gross_income_pct")[["state", "payment_share_of_gross_income_pct"]])
```

## Sources

U.S. Census Bureau ACS 2024 1-year tables B25077, B25103, B19013 (cross-checked against GCT2510 and ACSBR-025); Freddie Mac PMMS release of Oct 15, 2026.

## Cite

CalcWise (2026). *US Mortgage Affordability by State (2026)*, version 2026.1. https://www.calcwise.tools/reports/mortgage-affordability-by-state

## Changelog

- 2026.1 (2026-10-20): first release, ACS 2024. The ACS 2025 update follows the Census release of Oct 29, 2026.
