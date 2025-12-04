# SQL / Pandas Practice

## SQL
### SQL Optmization
...to be done 

## Pandas
### Pandas Chaining
As we already know, the SQL logical order is:

```
SQL Logical Order
1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. DISTINCT
7. ORDER BY
8. LIMIT
```

The database engine rearranges each query behind the scenes for maximum optimization. Even if we were to write `SELECT` first, the engine executes `WHERE` before it picks the columns.

In Pandas however, there is no hidden optimizer. Pandas executes strictly in the order you write it. Therefore this means we have to act as the query optimizer. To write efficient Pandas code (especially as a DE or MLE), we should manually mimic the SQL Logical Execution Order.

| **SQL Logical Order** | **Pandas Method Chain** | **Why this order?** |
| :--- | :--- | :--- |
| **1. FROM** | `df` | Start with the data. |
| **2. WHERE** | `.query(...)` or `.loc[...]` | **Filter rows immediately.** Don't process rows you don't need. |
| **3. GROUP BY** | `.groupby(...)` | Aggregate data. |
| **4. HAVING** | `.filter(...)` | Filter based on group properties. |
| **5. SELECT** | `[['col_a', 'col_b']]` or `.assign()` | **Drop unused columns.** Reduce memory usage. |
| **6. DISTINCT** | `.drop_duplicates()` | Remove dupes on the smaller dataset. |
| **7. ORDER BY** | `.sort_values(...)` | **Sort last.** Sorting is expensive ($O(N \log N)$); sort as few rows as possible. |
| **8. LIMIT** | `.head(...)` | Cut the data off at the very end. |

