# Use a join table in a delete statement

Sometimes you want to delete a thing conditionally.
Sometimes the condition lives on another table with a relationship to the table you are deleting rows from.
You can make the neccessary join for the statement using `USING`

```sql
DELETE FROM t1
USING t2
WHERE t1.t2_id = t1.id
AND <additional conditions>
```
