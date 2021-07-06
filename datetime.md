
# Datetime

- [MySQL Timezone Cheatsheet](https://gist.github.com/suvozit/bf0200bf7b5029ebe5f4)
- [MySQL Timezone documentation](https://dev.mysql.com/doc/refman/8.0/en/time-zone-support.html)



## Introduction

```sql

# get timezone in mysql
SELECT @@global.time_zone;
// -> SYSTEM or +00:00

# view current time 
SELECT now();
// -> 2021-06-04 19:41:00

# change tz in /etc/mysql/my.cnf
SET GLOBAL time_zone = 'America/New_York';
sudo service mysql restart

```

To see the `SYSTEM` time (works in Ubuntu)

```bash

# get timezone
cat /etc/timezone
// -> Etc/UTC

# get time 
date
// -> Fri Jun  4 19:41:00 UTC 2021

OR 

> node
> let d = new Date();
> d
2021-06-04T19:41:00.000Z

```





Select a range

```sql

# Greater than
SELECT * FROM table WHERE date_column > "2020-12-02";

# hour range
SELECT * FROM table WHERE date_column >= '2020-07-01 03:00:00' AND date_column <= '2020-07-01 04:00:00';

# month range
SELECT * FROM table WHERE date_column >= '2020-07-01' AND date_column <= '2020-07-31';

```
