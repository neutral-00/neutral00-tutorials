# Views

In PostgreSQL, a **View** is essentially a stored query. You can think of it as a "virtual table." It doesn't store the data physically; instead, it runs the underlying query every time you call the view.

### The Syntax

The basic syntax in PostgreSQL is:

```sql
CREATE [OR REPLACE] VIEW view_name AS
SELECT columns
FROM table
WHERE condition;

```

---

### Applying it to your Phone Data

If you want to turn that manufacturer average logic into a view so you don't have to rewrite the math every time, you would do this:

```sql
CREATE OR REPLACE VIEW manufacturer_price_stats AS
SELECT 
    manufacturer, 
    AVG(price) AS average_price,
    COUNT(*) AS total_models
FROM phones
GROUP BY manufacturer;

```

### How to use it

Once created, you treat it just like a regular table. To find that maximum average price again, your query becomes much shorter:

```sql
SELECT MAX(average_price) 
FROM manufacturer_price_stats;

```

---

### Key Things to Know

* **`OR REPLACE`**: This is highly recommended. It allows you to update the view definition without having to `DROP` it first (which would fail if other objects depend on it).
* **Real-time Data**: If you add a new phone to the `phones` table, the view will automatically reflect that change the next time you query it.
* **Security**: Views are great for security. You can give a user access to a view that hides sensitive columns (like `cost_price`) while still letting them see the `average_price`.

