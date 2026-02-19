# Filter with WHERE

Run the below query to get records whose area is greater than 4000.
```sql
SELECT name, area FROM cities WHERE area > 4000;
SELECT name, area FROM cities WHERE area BETWEEN 2000 AND 4000;
SELECT name, area FROM cities WHERE name IN ('Delhi', 'Shanghai');
SELECT name, area FROM cities WHERE name NOT IN ('Delhi', 'Shanghai');
```


In the WHERE clause we can use the following operators:
1. `=` - value equals
2. `>` - value greater than
3. `<` - value less than
4. `>=` - greater than or equal to
5. `<=` - less than or equal to
6. `IN` - is the value in a list
7. `<>` - value not equal to
8. `!=` - value not equal to
9. `BETWEEN` - value is between two values
10. `NOT IN` - value is not in a list


## WHERE with Calculations

```sql
SELECT name, area / population AS population_density FROM cities
  WHERE area / population > 6000;
```
