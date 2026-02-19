# Groupings and Aggregations

## Aggregation
> **Aggregation is a process that uses aggregate functions to return a single value from multiple rows.**

For example:

```sql
SELECT SUM(salary) FROM employees;
```

Here:

* `SUM()` is the aggregate function.
* It takes multiple salary values (multiple rows).
* It returns one single value.

---

### Even Simpler Version

> Aggregation means calculating a single result (like sum, count, or average) from multiple rows.

---

Look out for words : most/average/least/count etc.

## Example

1. Find the most viral photo i.e. the photo with the highest number of comments.

### Common Aggregation Functions

| Function | Description |
| --- | --- |
| **COUNT()** | Returns the number of rows that match a criteria. |
| **SUM()** | Calculates the total sum of a numeric column. |
| **AVG()** | Calculates the average value of a numeric column. |
| **MIN() / MAX()** | Finds the lowest or highest value in a set. |

---

### How it Works

Aggregations are almost always paired with the **`GROUP BY`** clause, which organizes the data into buckets before the calculation is applied.

> **Pro Tip:** Remember that aggregate functions (except for `COUNT(*)`) usually ignore `NULL` values in their calculations.


## Groupings
> **Grouping is putting rows that have the same value in one or more columns together.**
- uses the keyword `GROUP BY` followed by one or more column names

### Small clarification

* If you group by **one column**, rows with the same value in that column are grouped.
* If you group by **multiple columns**, rows must match in *all* those columns to be in the same group.

Example:

```sql
GROUP BY Department, JobTitle
```

Here, rows are grouped only if **both Department AND JobTitle are the same**.


In grouping, visualizing the result is the key.
- example on a phones table:
```
+-------------+--------------+-------+------------+
| name        | manufacturer | price | units_sold |
+-------------+--------------+-------+------------+
| N1280       | Nokia        | 199   | 1925       |
+-------------+--------------+-------+------------+
| Iphone 4    | Apple        | 399   | 9436       |
+-------------+--------------+-------+------------+
| Galaxy S    | Samsung      | 299   | 2359       |
+-------------+--------------+-------+------------+

```
```sql
SELECT name
FROM phones
GROUP BY manufacturer
```

The above query will result in an error because we have to use an aggregate function to select a non-grouped column.
How about the below one:
```sql
SELECT manufacturer
FROM phones
GROUP BY manufacturer;
```

This is will return records and won't error because we selected a grouped column.

Here are some of the aggregate functions:
1. `COUNT()` returns the number of values in a group.
1. `SUM()` finds the sum of a group of numbers.
1. `AVG()` finds the average of a group of numbers.
1. `MIN()` returns the minimum value from a group of numbers.
1. `MAX()` returns the maximum value from a group of numbers.

Example queries:
```sql
SELECT MAX(id)
FROM comments;

-- check how many photos we have
SELECT COUNT(id)
FROM photos;
```

## ⚠️ Warning
- You can not select a column used in an aggregate function as is like the below query
```sql
SELECT COUNT(id), id
FROM photos;
```
- This will throw some error like: `column "photos.id" must appear in the GROUP BY clause or be used in an aggregate function`


## Combining Group By and Aggregations
Let's release the super power of group by combined with aggregations.
When we run this query: `SELECT user_id FROM comments GROUP BY user_id`

Essentially visualise as:

| grouped_user_id | id | contents                | user_id | photo_id |
| --------------- | -- | ----------------------- | ------- | -------- |
| 1               | 1  | Non est totam           | 1       | 5        |
| 1               | 7  | Non est totam           | 1       | 5        |
| 2               | 5  | Quo velit iusto ducimus | 2       | 4        |
| 2               | 6  | Voluptas ab eius.       | 2       | 5        |
| 3               | 2  | Sed cumque in et.       | 3       | 5        |
| 3               | 4  | Enim esse magni.        | 3       | 5        |
| 5               | 3  | Et sit occaecati.       | 5       | 5        |

Remember we can't select id or contents or photo_id.

Now from this data, we can find the latest id of comment for each user using the `MAX()` as shown
```sql
SELECT user_id, MAX(id)
FROM comments
GROUP BY user_id;
```

### COUNT
Next let's find out how many comments each user have commented.
```sql
SELECT user_id, COUNT(id)
FROM comments
GROUP BY user_id;
-- OR count the number of rows of each group
SELECT user_id, COUNT(*)
FROM comments
GROUP BY user_id;
```


Next find the number of comments for each individual photo.
In the comments table we have a photo_id let's group by it and use the count aggregation.
```sql
SELECT photo_id, COUNT(*)
FROM comments
GROUP BY photo_id;
```


One more example:

Write a query that will print an author's id and the number of books they have authored.
```
#### authors
+----+-----------------+
| id | name            |
+----+-----------------+
| 1  | JK Rowling      |
+----+-----------------+
| 2  | Stephen King    |
+----+-----------------+
| 3  | Agatha Christie |
+----+-----------------+
| 4  | Dr Seuss        |
+----+-----------------+

#### books
+----+---------------------+-----------+
| id | title               | author_id |
+----+---------------------+-----------+
| 1  | Chamber of Secrets  | 1         |
+----+---------------------+-----------+
| 2  | Prisoner of Azkaban | 1         |
+----+---------------------+-----------+
| 3  | The Dark Tower      | 2         |
+----+---------------------+-----------+
| 4  | Murder At the Links | 3         |
+----+---------------------+-----------+
| 5  | Affair at Styles    | 3         |
+----+---------------------+-----------+
| 6  | Cat in the Hat      | 4         |
+----+---------------------+-----------+

```

Let's write the query:
```sql
SELECT author_id, COUNT(*)
FROM books
GROUP BY author_id;
```

Next instead of author_id display the author name instead.
```sql
SELECT name, COUNT(*)
FROM books
JOIN authors ON authors.id = books.author_id
GROUP BY author_id,authors.name;
-- OR you could have done
SELECT name, COUNT(*)
FROM books
JOIN authors ON authors.id = books.author_id
GROUP BY authors.name;
```

