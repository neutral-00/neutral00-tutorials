# Delete User Scenarios

Note that user id is a foreign key in photos table.

What happens when we try to delete a user referenced by the photos table?

Below are the `On Delete Options` we have:
1. `ON DELETE RESTRICT` - this will throw an error.
1. `ON DELETE NO ACTION` - this will throw an error.
1. `ON DELETE CASCADE` - this will delete associated records in photos table too.
1. `ON DELETE SET NULL` - this will set the user_id to NULL in photos table.
1. `ON DELETE SET DEFAULT` - this will set the user_id to default value if provided in photos table.


To test out the above scenarios we will drop and recreate the photos table several times. \
So keep the below snippets handy.
```sql
CREATE TABLE photos (
id SERIAL PRIMARY KEY,
url VARCHAR(200),
user_id INTEGER REFERENCES users(id)
);
 
INSERT INTO photos (url, user_id)
VALUES
('http:/one.jpg', 4),
('http:/two.jpg', 1),
('http:/25.jpg', 1),
('http:/36.jpg', 1),
('http:/754.jpg', 2),
('http:/35.jpg', 3),
('http:/256.jpg', 4);
```

Next let's drop the photos table.
```sql
DROP table photos;
```


## ON DELETE CASCADE - Scenario

```sql
CREATE TABLE photos (
id SERIAL PRIMARY KEY,
url VARCHAR(200),
user_id INTEGER REFERENCES users(id) ON DELETE CASCADE
);
 
INSERT INTO photos (url, user_id)
VALUES
('http:/one.jpg', 4),
('http:/two.jpg', 1),
('http:/25.jpg', 1),
('http:/36.jpg', 1),
('http:/754.jpg', 2),
('http:/35.jpg', 3),
('http:/256.jpg', 4);
```

Run `DELETE FROM users WHERE id = 1;` then query the photos table and see for yourself what happened.

## ON DELETE SET NULL - Scenario

```sql
DROP TABLE photos;
CREATE TABLE photos (
id SERIAL PRIMARY KEY,
url VARCHAR(200),
user_id INTEGER REFERENCES users(id) ON DELETE SET NULL
);
 
INSERT INTO photos (url, user_id)
VALUES
('http:/one.jpg', 4),
('http:/754.jpg', 2),
('http:/35.jpg', 3),
('http:/256.jpg', 4);
```

Next let's delete user with id 4 and see what happens in photos table.
```sql
DELETE FROM users
WHERE
	id=4;
```

Check `SELECT * FROM photos;`
