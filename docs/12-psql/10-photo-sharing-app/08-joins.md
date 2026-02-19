# JOINS

Joins produces values by merging together records from different related tables.

## Example

1. Find all the comments for the photo with id = 3 along with the username of the comment author.
1. Find photo with id = 10 and the comments attached to it.

## 🛈 Info
- We can use table alias to assist shortening reference to columns
- For this, use the `AS` keyword followed by the alias or directly followed by alias after the table name.

Example:
```sql
SELECT title, name FROM books b
JOIN authors AS a ON a.id = b.author_id;
```

But note that putting `AS` adds more clarity that something is aliasing here.
Use the alias to give context to column names in case of same column names in multiple tables.
