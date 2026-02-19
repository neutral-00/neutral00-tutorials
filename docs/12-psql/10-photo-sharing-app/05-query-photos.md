# Query Photos Table


Let's get some meaningful data from our tables.

1. Find all the photos created by user with id 4.
```sql

SELECT * FROM photos
WHERE
	user_id=4;
```


2. List all the photos along with associated user details.
```sql
SELECT * FROM photos
JOIN users ON users.id = photos.user_id;

-- OR
 SELECT url, username FROM photos
 JOIN users ON users.id = photos.user_id;
```


## Observe
1. In the second query, url is from photos table and username is from users table.
