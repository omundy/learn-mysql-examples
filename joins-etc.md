
## Joins, Unions, etc.

#### References

* [Union](https://www.w3schools.com/sql/sql_union.asp)
* [Join](https://www.w3schools.com/sql/sql_join.asp)



<img src="https://i.stack.imgur.com/LSPyQ.png" />

```sql

# union - combine data into new rows from one or more TABLES using two or more select statements

SELECT 23 AS bah 
UNION
SELECT 45 AS bah;
+-----+
| bah |
+-----+
|  23 | 
|  45 | 
+-----+

# select condition from a union, with union all to allow duplicate values 

SELECT * FROM
(
  SELECT type, name FROM attacks as a
  UNION ALL
  SELECT type, name FROM badges as b
) result
WHERE createdAt = "2020-07-01"
ORDER BY createdAt DESC; 


```

<img src="https://i.stack.imgur.com/l4hxo.png" />

```sql

# join - joins combine data into new columns from one or more TABLES using a cartesian product

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






```sql
# update one column in a table with data from the same table

UPDATE consumables t1 
JOIN consumables t2 ON t1.id = t2.id
SET t1.slug = CONCAT(t2.name, "-", t2.type) WHERE t1.id = 371;

```
