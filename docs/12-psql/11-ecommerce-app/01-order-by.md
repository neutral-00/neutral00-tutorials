# Order by

```sql
SELECT * FROM products
ORDER BY price;
-- OR
SELECT * FROM products
ORDER BY price DESC;
```

Default is `ASC`.

Let's have example of `ORDER BY` on multiple columns.
```sql
SELECT * FROM products
ORDER BY price, weight;
```
