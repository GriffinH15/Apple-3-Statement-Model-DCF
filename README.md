# Apple (APPL) 3-statement model and DCF Valuation

A 3-statement financial model (Income Statement, Balance Sheet, Cash Flow 
Statement) and discounted cash flow valuation for Apple Inc., built as a 
personal project to practice financial modeling.

## What's in this model:
- 5 Year forecast (2026-2030) based off of 10-K filings (2023-2025)
- Fully linked 3 financial statements, including forecast years with dynamic formulas and calculations
- DCF Valuation using unlevered free cash flow, discounted with WACC
- WACC built from historical assumptions + CAPM, Equity Value, and calculations of cost of equity, % of equity and debt
- Two Variable Sensitivity Table, using Terminal Growth Rate and WACC

## Key assumptions
- Revenue Growth: 8% (After testing against a 5% growth rate)
- Gross Margin: 46.5% (Held flat for forecast years)
- WACC: ~10.1%
- Terminal Growth Rate: 3.5%
- 15.5% Tax Rate

## 3-Statement Model 
- Built AR, Inventory, AP off of ratios instead of hardcoding. This allowed me to have my spreadsheet connected to real values, like revenue and COGS, so if revenue or COGS were to change, the accounts dependent on them would also change, which represents what could happen in a real company if finances get altered for a variety of reasons.
- My forecasting "cash and equivalents" for the balance sheet is taken right from the ending balance in the SCF. This helped to show me how the statements are connected and how finance theory is translated to real world money and companies. I did this instead of hardcoding in a cash assumption is because that wouldn't allow my sheet to update if the SCF was updated, and cash changed hands in a different manner. This would lead to the balance sheet becoming unbalanced and someone would need to go into the model and manually update the cash every time it changes in the SCF, which is tedious and time consuming and leads for a chance of human error.
- PP&E Roll forward was calculated as previous year PP&E - depreciation + CAPEX. This is a better way to calculate PP&E vs. basing it as a % of revenue, since CAPEX is what is used to attain more PP&E, and depreciation shows how current PP&E is losing value over time. You add these to the previous PP&E to show how the total balance is updating over time, and it is more accurate than using revenue, since revenue could increase without PP&E increasing, and if you linked them together this could inflate PP&E artificially.

## DCF valuation and Key Findings
- Implied Share Price: $134.70 vs. actual (9/4/26) of $319.97
- Majority of company is Equity (97.8%) compared to debt (2.2%)
- In the Sensitivity Table, an increase in TGR caused the implied share price to increase more with every 0.5% jump, while an increase in WACC caused the share price to drop by a smaller % each time. This is because increasing the TGR makes the denominator smaller in the terminal value calculation, leading to a bigger and potentially overinflated share price. With the WACC increasing, this makes the denominator bigger, leading to a smaller share price with an increasing WACC. The risk of this in a DCF model is if TGR overtakes WACC, implied share price will be negative, and if TGR equals WACC, you will be dividing by 0 and get an error.

## Debugging
- Balance sheet had an error with forecasting, where all but one year would balance. I fixed this by combing through my formulas, and seeing that I had correctly copied across. This led me to see that it was a rounding error causing the issue, since these formulas lead to numbers with 5+ decimals and my balance checker required an exact match. I then changed my "balance checker" formula from IF to IF with ROUND, which fixed this decimal discrepancy.
- When finding present value of FCF, my formula wasn't referencing the changing years, and was referencing nothing, leading to the same value result from discounting using WACC. I fixed this by making sure my formulas were actually locked using the $ symbol for both the row and column, which allowed me to reference the single WACC cell but change the result based on the amount of years I was discounting by. 
- My sensitivity Table had a circular reference because I used the actual TGR and WACC values as a reference in the table instead of hardcoding. This led to the values under those columns to not change from the previous values, giving me an inaccurate view on how changing TGR and WACC affects the implied share price. Instead of referencing the cell in my spreadsheet, I manually entered the WACC of 10.1% and TGR of 3.5% to prevent the circular reference from occuring, leading to an accurate portrayal of the share price.
