# Insert Data

As we discussed earlier, let's consider the below data from the wiki for insertion
| name | country | population | area |
| --------------- | --------------- | --------------- | --------------- |
| Tokyo | Japan | 38_50_5000 | 8223 |
| Delhi | India | 28_12_5000 | 2240 |
| Shanghai | China | 22_12_5000 | 4015 |
| Sao Paulo | Brazil | 20_93_5000 | 3043 |

Run the below insert query
```sql
INSERT INTO cities (name, country, population, area) 
VALUES 
	('Tokyo', 'Japan', 38505000, 8223),
  ('Delhi', 'India', 28125000, 2240),
  ('Shanghai', 'China', 22125000, 4015),
  ('Sao Paulo', 'Brazil', 20935000, 2043);
```


