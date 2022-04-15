# Get the size of all indexes in megabytes

If you want to get the size of all indexes here's a query to run. Courtesy of [Daniela Zohar's StackOverflow answer][1].

```sql
SELECT database_name, table_name, index_name,
ROUND(stat_value * @@innodb_page_size / 1024 / 1024, 2) size_in_mb
FROM mysql.innodb_index_stats
WHERE stat_name = 'size' AND index_name != 'PRIMARY'
ORDER BY size_in_mb DESC;
```

[1]:https://stackoverflow.com/a/36573801
