# Create an index without blocking writes in postgres

Postgres will lock writes on a table while it is creating an index by default.
That means it will not allow any insert/update/delete operations.
If you would like to _not_ lock writes on the table you have to say the magic word: `CONCURRENTLY`

```sql
CREATE INDEX CONCURRENTLY sales_quantity_index ON sales_table (quantity);
```

There are caveats:

* You **cannot** run this in a transaction (you'll have to [take steps in Rails migrations], which are wrapped in a transaction by default).
* Postgres will wait for any pending transactions that effect the table to terminate first (that's a simplification).
* Postgres will make two scans and take considerably longer to complete the operation than it would adding a basic index.
* It will create additional load on the database that may effect performance for other operations.
* If the operation fails (for a uniqueness constraint violation, for example) the `CREATE INDEX` operation will fail but still leave behind an invalid index that you'll have to clean up manually.

Read about the caveats in more detail [in the docs].

[take steps in Rails migrations]:https://thoughtbot.com/blog/how-to-create-postgres-indexes-concurrently-in
[in the docs]:https://www.postgresql.org/docs/14/sql-createindex.html#SQL-CREATEINDEX-CONCURRENTLY
