# Create test data in postgres with `generate_series` and `random`

The `generate_series` function in postgres lets you create a series of values.
You can use it to generate a lot of test data.
This is useful when playing around with benchmarks that require a larger data set to be more useful.

The `RANDOM()` function is useful when you need to create some variety in the generated values.
The `RANDOM()` function will return a number from 0.0 up to and including 1.0.
It works when used with date and time values, too:

```bash
psql=# select interval '30 days' * random() as ran_timestamp;
      ran_timestamp
-------------------------
 27 days 16:51:53.610641
(1 row)
```

Example usage for generating some random token data:

```sql
CREATE TABLE login_token(
  id serial primary key,
  valid_until timestamp not null
);

INSERT INTO login_token(valid_until)
SELECT (NOW() + (RANDOM() * interval '1 hour') - interval '30 minutes')
FROM generate_series(1,100000);
```
