# Sub-query

We can use Sub-query inside
1. SELECT clause
2. FROM clause
3. JOIN clause
4. WHERE clause


> [!NOTE]
> We much use an alias of the result of the sub-query when used inside a FROM clause.


## Example 1
Calculate the average price of phones for each manufacturer.  Then print the highest average price. Rename this value to max_average_price.

```sql
SELECT MAX(p.average_price) AS max_average_price
FROM (
    SELECT manufacturer, AVG(price) AS average_price
    FROM phones
    GROUP BY manufacturer
) AS p;
```

Or If you want common table expression
```sql
WITH ManufacturerAverages AS (
    SELECT manufacturer, AVG(price) AS average_price
    FROM phones
    GROUP BY manufacturer
)
SELECT MAX(average_price) FROM ManufacturerAverages;
```
