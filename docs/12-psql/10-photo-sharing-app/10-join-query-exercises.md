# Query Exercise

## 1. Find comments and usernames.

Note that comments are present in the comments table and usernames are present in users table.
We should use JOIN.

```sql
SELECT
  contents,
  username
FROM
  comments
  JOIN users ON users.id = comments.user_id;
```


## 2. Find photos and associated comments

Here also we will use JOIN as photos are in photos table and comments in comments table.
Also note that photo_id is a foreign key in comments table.
```sql
SELECT
  url,
  contents
FROM
  comments
  JOIN photos ON photos.id = comments.photo_id;
```


## 3. Find photos and associated users.

But before running your actual query run the below insert statement:
```sql
INSERT INTO photos(url, user_id)
VALUES ('https://banner.jpg', NULL);
```


Now write your query, selecting the photo url and username.
```sql
SELECT url, username FROM photos
JOIN users ON users.id = photos.user_id;
```

### Observation
- Did you observe that the result didn't include our last record?
- This is where we need to know the types of JOINS.
