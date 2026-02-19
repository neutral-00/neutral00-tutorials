# String Operations

We have some of the string operations and functions:
1. `||` - Join two strings
2. `CONCAT()` - Join two strings
3. `LOWER()` - Convert to lowercase
4. `UPPER()` - Convert to UPPERCASE
5. `LENGTH()` - Gives the number of letters in the string.

Let's try joining strings.
```sql
SELECT name || ', ' || country AS location FROM cities;
-- OR using CONCAT
 SELECT CONCAT(name, ', ', country) AS location FROM cities;
```
