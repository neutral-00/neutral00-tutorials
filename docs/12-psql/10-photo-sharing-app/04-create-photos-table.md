# Create Photos Table


Next let's create photos table with user's id as the foreign key.
```sql
CREATE TABLE photos (
	id SERIAL PRIMARY KEY,
  url VARCHAR(200),
  user_id INTEGER REFERENCES users(id)
);
```


Let's insert some data keeping our foreign key in mind.
```sql
INSERT INTO photos (url, user_id)
VALUES
	('https://one.jpg', 4),
	('https://two.jpg', 1),
  ('https://25.jpg', 1),
  ('https://36.jpg', 1),
  ('https://754.jpg', 2),
  ('https://35.jpg', 3),
  ('https://256.jpg', 4);


SELECT * FROM photos;
```



