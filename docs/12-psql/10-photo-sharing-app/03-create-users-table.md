# Create Users Table


Create the users table as shown below:
```sql
CREATE TABLE users (
	id SERIAL PRIMARY KEY,
  username VARCHAR(100)
);
```


## Observe
1. `id` column is a SERIAL. So our db will take care of it.

## Insert some data
```sql
 INSERT INTO users (username)
 VALUES
 	('monahan93'),
  ('pfeffer'),
  ('si93onis'),
  ('99stroman');


 SELECT * FROM users;
```
