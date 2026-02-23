# Offset

It means skip the number of rows specified using the `OFFSET` keyword.

Example:
```sql
SELECT * FROM USERS
OFFSET 40;
```

This means skip the first 40 records from the users table.

## LIMIT
It means select only the specified number of rows from a result set.

Example: Find the 5 most expensive products
```sql
SELECT * 
FROM products
ORDER BY price DESC
LIMIT 5;
```

How about the next set of 5 most expensive products?
```sql
SELECT * 
FROM products
ORDER BY price DESC
LIMIT 5
OFFSET 5;
```

## 🤔 Observation
- Notice that as a convention we put `LIMIT` first and then `OFFSET`

## One more example.
Find the 2nd and 3rd most expensive phones.
```sql
SELECT name
FROM phones
ORDER BY price DESC
LIMIT 2
OFFSET 1;
```
