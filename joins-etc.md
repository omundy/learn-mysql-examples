
## Joins, Unions, etc.

#### References

* [Union](https://www.w3schools.com/sql/sql_union.asp)
* [Join]((https://www.w3schools.com/sql/sql_join.asp))



```sql

# union - combine rows using two more select statements

SELECT 23 AS bah 
UNION
SELECT 45 AS bah;
+-----+
| bah |
+-----+
|  23 | 
|  45 | 
+-----+

# join - combine rows AND columns from two more TABLES using a cartesian product

SELECT * FROM 
(SELECT 23 AS bah) AS foo 
JOIN 
(SELECT 45 AS bah) AS bar
ON (33=33);
+-----+-----+
| foo | bar |
+-----+-----+
|  23 |  45 | 
+-----+-----+



```
