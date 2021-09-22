# User partial indexes

Scenario: 
You have a `users` table and an `activated` column that flags when users have taken the action necessary to activate their new account.
Most of your users, let's say ~90%, have activated their accounts.
You have some process that is querying against this table to find unactivated user accounts.

First, you create an index on `users.activated`. This is a rather large index on disk since the `users` table is huge.
It works, though. Youre query is faster.

But you can improve things by dropping that index and creating a partial index instead.
A partial index includes a predicate like this:

```sql
CREATE INDEX users_unactivated_partial_index ON users(id)
WHERE not activated;
```

This will result in a much smaller index on disk.

A partial index is generally useful whenever you want to be doing queries against a subset of a table.
It is particularly useful in our scenario, as the first index would not even be used for queries selecting activated users as ~90% of rows are activated and the index is not useful.

[Read More](https://hakibenita.com/sql-tricks-application-dba#use-partial-indexes) and [check out the docs](https://www.postgresql.org/docs/8.0/indexes-partial.html).
