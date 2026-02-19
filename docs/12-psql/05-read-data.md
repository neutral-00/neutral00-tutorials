# Read Data

Run the below queries to fetch data
```sql
-- SELECT * FROM cities;
SELECT name, population FROM cities;
```


## Observation
1. Observe that `--` is used to comment a line.


## Info
1. Note that area is in square kilometers.


## Problem Statement - 1 calculate population density for each record

Calculate the population density i.e. population/area

```sql
SELECT name, population/area FROM cities;
-- OR even better
SELECT name, population/area AS population_density
FROM cities;

```

We can also use the following operations:
1. `+` - Add
2. `-` - Subtract
3. `*` - Multiply
4. `/` - Divide
5. `^` - Exponent
6. `|/` - Square root
7. `@` - Absolute value
8. `%` - Remainder
