# All Dax Function
## 📐 Core DAX Measures  


- 1. Average SQM Price
```DAX
AVG SQM Price = AVERAGE(Housing[sqm_price])
```
- 2. Offer to SQM Ratio
```
Offer to SQM Ratio = DIVIDE(SUM(Housing[Offer price]), SUM(Housing[sqm]))
```
- 3. Sales by Region
```
Sales by region =
    CALCULATE(SUM(Housing[purchase_price]),
              ALLEXCEPT(Housing, Housing[region]))
```
- 4. Total YTD Sales
```
Total YTD Sales =
    TOTALYTD(SUM(Housing[purchase_price]), Housing[date].[Date])
```
- 5. Last 12 Month Sales
```
Last 12 Month Sales =
    CALCULATE(SUM(Housing[purchase_price]),
              DATESINPERIOD(Housing[date], MAX(Housing[date]), -12, MONTH))
```
- 6. Median Sales Price Change (YoY)
```
Median Sales Price Change =
VAR curMedian =
    MEDIANX(FILTER(Housing, YEAR(Housing[date].[Date]) = YEAR(MAX(Housing[date].[Date]))),
            Housing[purchase_price])
VAR prevMedian =
    MEDIANX(FILTER(Housing, YEAR(Housing[date].[Date]) = YEAR(MAX(Housing[date].[Date])) - 1),
            Housing[purchase_price])
RETURN
    IF(prevMedian <> 0, (curMedian - prevMedian) / prevMedian, BLANK())
```
- 7. Units Sold (Latest YQ)
```
Units Sold (Latest YQ) =
    CALCULATE(DISTINCTCOUNT(Housing[house_id]),
              YEAR(Housing[date]) = YEAR(MAX(Housing[date]))
              && QUARTER(Housing[date]) = QUARTER(MAX(Housing[date])))
```
- 8. YoY Sales Growth
```
YOY Sales Growth =
VAR currYear =
    CALCULATE(SUM(Housing[purchase_price]),
              YEAR(Housing[date]) = YEAR(MAX(Housing[date])))
VAR prevYear =
    CALCULATE(SUM(Housing[purchase_price]),
```
