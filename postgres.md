# PostgreSQL

## Update a table with information from a joined table

I frequently need to do this when adding a new column to a table that is non-nullable.
For example, adding a `last_modified_by_id`.
But for an existing table with records, you can't just add the non-nullable column!
Instead, you need to:

- create the column as nullable, 
- then update all the records so that the new column has no null values, 
- then set the column to `NOT NULL` when you're done.

Often the data I want to save as the starting value can be found on a joined table.
To join on a table to use its values in the `UPDATE`, you would do the following:

```sql
UPDATE child_table
SET parent_name = parent_table.name
FROM parent_table WHERE parent_table.id = child_table.parent_id
```

- `UPDATE` sets the one and _only_ table that will be altered.
- `FROM` points to the table you're joining on
- `WHERE` clause is equivalent to the `JOIN x ON y` of a typical `JOIN`
