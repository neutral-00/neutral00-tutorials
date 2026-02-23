# EXCEPT

It keeps the rows that are present only in the result set of the first query.

```sql
(
SELECT * 
FROM products
ORDER BY price DESC
LIMIT 4
)
EXCEPT
(
SELECT *
FROM products
ORDER BY price/weight DESC
LIMIT 4
);
```


