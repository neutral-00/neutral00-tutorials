# UNION

It combines two result sets. By default if a record is present in both result sets, only one is shown.

In case you want to show as duplicate then use `UNION ALL`.

## Example:
List 4 most expensive products and 4 products with the most efficient price/weight ratio.
```sql
(
SELECT * 
FROM products
ORDER BY price DESC
LIMIT 4
)
UNION
(
SELECT *
FROM products
ORDER BY price/weight DESC
LIMIT 4
);
```

## Example 2:
Write a query that will print the manufacturer of phones where the phone's price is less than 170.  Also print all manufacturer that have created more than two phones.

IMPORTANT: You don't need to wrap each query with parenthesis! Your solution should not have any parens in it.

```sql
SELECT manufacturer
FROM phones
WHERE price < 170
UNION
SELECT manufacturer
FROM phones
GROUP BY manufacturer
HAVING count(*) > 2;
```
