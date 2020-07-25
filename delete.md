## Delete

#### References

* [MySQL DELETE JOIN](https://www.mysqltutorial.org/mysql-delete-join/)




```sql

# delete random row from one table with subquery from another 

DELETE FROM table1
WHERE guid IN (
  SELECT guid FROM table2 t2
  WHERE t2.tester = 1
)
ORDER BY RAND() 
LIMIT 1;

```
