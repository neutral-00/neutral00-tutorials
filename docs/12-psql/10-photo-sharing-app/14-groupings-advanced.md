# Grouping - Advanced

## NOTES
1. `JOIN` merges data from additional tables.
1. `WHERE` filters the set of rows.
1. `GROUP BY` groups rows by a unique set of values.
1. `HAVING` filters the set of groups.


## Scenario - 1
Find photos with more than 2 comments and photo id less than 3.

```sql
SELECT photo_id, COUNT(*)
FROM comments
WHERE photo_id < 3
GROUP BY photo_id
HAVING COUNT(*) > 2;
```


## Scenario - 2
Find users who commented more than two times in their initial two photos.

