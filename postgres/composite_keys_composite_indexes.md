# Composite keys and composite indexes (in postgresql)

Usually you'll identify a unique record by a single column that holds a unique number (which the database will autoincrement on a new row write).
But sometimes you'll want to identify a record by a combination of values.
For example, friendship.

A friendship could be modeled in a number of ways in your database, but a composite primary key works well since the relationship is bi-directional.
To create a table with a composite primary key you'll specify the columns as arugments to `PRIMARY KEY()` as so:

```sql
CREATE TABLE friendships (
    friend_a_id integer NOT NULL REFERENCES users (id),
    friend_b_id integer NOT NULL REFERENCES users (id),
    PRIMARY KEY(friend_a, friend_b) -- Here we set the composite primary key
);
```

## Considerations

Postgres will automatically create an index for the composite primary key.
It will be optimized for queries with conditions on `(friend_a_id)`, `(friend_a_id, friend_b_id)`.
Queries for conditions on `(friend_b_id)` alone will be less efficient but still optimized.

e.g., if you set `PRIMARY KEY(a,b,c)`, the indexes are optimized for queries with conditions on `(a)`, `(a, b)`, and `(a, b, c)` and less optimized for queries `(b), (b, c), (c), (a,c)`.

You can create additional (composite) indices with a different order if queries on conditions `(b, c)` need to be speedy as well.
