# Joins 3 tables

Now that we know the different types of joins, let's up skill even further our querying skills.

## Scenario - 1 Find all the photos where the user themselves have put comments.

Many a times, user might post a photo and put their own comments on the posted photo. Find such photos.
Select url, comment text i.e. `content` and username.

```sql
SELECT url, contents, username
FROM comments
JOIN photos ON photos.id = comments.photo_id
JOIN users ON users.id = comments.user_id AND users.id = photos.user_id;
```


## Scenario - 2 find books which have reviews by author themselves.
Try one more. You are working with a database of books, authors, and reviews

Write a query that will return the title of each book, along with the name of the author, and the rating of a review.  Only show rows where the author of the book is also the author of the review.

```
### authors
+----+-----------------+
| id | name            |
+----+-----------------+
| 1  | Stephen King    |
+----+-----------------+
| 2  | Agatha Christie |
+----+-----------------+
| 3  | JK Rowling      |
+----+-----------------+
### books
+----+---------------------+-----------+
| id | title               | author_id |
+----+---------------------+-----------+
| 1  | The Dark Tower      | 1         |
+----+---------------------+-----------+
| 2  | Affair At Styles    | 2         |
+----+---------------------+-----------+
| 3  | Chamber of Secrets  | 3         |
+----+---------------------+-----------+

### reviews
+----+--------+-------------+---------+
| id | rating | reviewer_id | book_id |
+----+--------+-------------+---------+
| 1  | 3      | 1           | 2       |
+----+--------+-------------+---------+
| 2  | 4      | 2           | 1       |
+----+--------+-------------+---------+
| 3  | 5      | 3           | 3       |
+----+--------+-------------+---------+
```
```


Write your query here:
```sql
SELECT b.title, a.name, r.rating
FROM reviews AS r
JOIN books AS b ON b.id = r.book_id
JOIN authors AS a ON a.id = b.author_id AND a.id = r.reviewer_id;
```
