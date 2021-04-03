# Conditional logic in a `SELECT` statement with `CASE`

The `CASE` statement allows you to use conditional logic in your `SELECT`
statement ([postgres docs]). This came in useful for me when building a query that was exported as
part of a data migration into another system's schema.

The `CASE` statement fits into the `SELECT` as if it were any other field:

```sql
SELECT * FROM people;

name  | age
------------
Greg  | 36
Lucas | 6

SELECT name,
       CASE WHEN age < 21 THEN 'water'
            ELSE 'wine'
       END beverage
FROM people;

name  | beverage
----------------
Greg  | 'wine'
Lucas | 'water'
```

[postgres docs]:https://www.postgresql.org/docs/13/functions-conditional.html#FUNCTIONS-CASE


