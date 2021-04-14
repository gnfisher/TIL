# Indexes and soft deletes

A soft delete is when you don't *really* destroy a record when a user deletes
it. Instead, you might set a timestamp value in the `deleted_at` column of the
table. If that column is `null`, then it's fair game to query. But if it's `NOT
NULL`, pretend it doesn't exist.

If you have a lot of "deleted" records in a big table, you might want to create
a [partial index][1]. This allows queries that search for a subset of data on a
table to perform the query more efficiently.

Given a table `people` of:
```sql
id | name  | deleted_at
----------------------
1  | Greg  | NULL
2  | Lucas | 2021-03-29 19:29:04.917659
```

We could create a partial index like this:
```sql
CREATE INDEX active_people_index ON people (deleted_at)
    WHERE deleted_at IS NOT NULL;
```

[1]:https://www.postgresql.org/docs/13/indexes-partial.html
