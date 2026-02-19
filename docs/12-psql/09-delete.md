# Delete

Let's delete the record of Tokyo.
```sql
DELETE FROM cities WHERE name = 'Tokyo';
```



Putting the record back
```sql
INSERT INTO cities (name, country, population, area)
VALUES ('Tokyo', 'Japan', 38505000, 8223);
```
