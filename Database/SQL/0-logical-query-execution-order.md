### Execution order in SQL (this is the key)
1. `FROM`
2. `WHERE` ← row-level filtering happens **here**
3. `GROUP BY`
4. `HAVING`
5. `SELECT`
6. `ORDER BY`