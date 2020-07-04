
## Dates

#### References

* 



```sql

# hour range
SELECT * FROM table WHERE date_column >= '2020-07-01 03:00:00' AND date_column <= '2020-07-01 04:00:00';

# month range
SELECT * FROM table WHERE date_column >= '2020-07-01' AND date_column <= '2020-07-31';
