# Create test data in postgres with `generate_series`

The `generate_series` function in postgres lets you create a series of values.
You can use it to generate a lot of test data.
This is useful when playing around with benchmarks that require a larger data set to be more useful.

Example usage:

```sql
CREATE TABLE login_token(
  id serial primary key,
  valid_until timestamp not null
);

INSERT INTO login_token(valid_until)
SELECT (NOW() + (RANDOM() * interval '1 hour') - interval '30 minutes')
FROM generate_series(1,100000);
```
