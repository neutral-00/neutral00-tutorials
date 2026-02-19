# Primary and Foreign Keys

A primary key is a special column that uniquely identifies a record in a table


A foreign key is a column that identifies a record usually in another table.

## 💡NOTE - Primary Key
1. Each row in a table has a primary key.
1. 99% of the time the column is called id
1. id value will be either integer or UUID


## 💡NOTE - Foreign Key
1. Rows only have it if they belong to another record.
1. Many records in the same table can have same foreign key.
1. Usually named like `xyz_id`
1. It is the primary key of the other table.
1. It will change if the relationship changes.
