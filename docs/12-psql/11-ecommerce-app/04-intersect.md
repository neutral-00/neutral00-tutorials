# INTERSECT

It finds the rows common in the result sets of two queries.

```sql
(
SELECT * 
FROM products
ORDER BY price DESC
LIMIT 4
)
INTERSECT
(
SELECT *
FROM products
ORDER BY price/weight DESC
LIMIT 4
);
```
