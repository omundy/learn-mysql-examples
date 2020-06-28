
## Strings



```sql

# basic substring examples
SELECT SUBSTRING_INDEX('hello world!',' ', 1); # hello
SELECT SUBSTRING_INDEX('http://www.test.com/path/','://', -1); # www.test.com/path/ 


# get ONLY the domain name and TLD from url 
SELECT SUBSTRING_INDEX(
            SUBSTRING_INDEX(
               	SUBSTRING_INDEX(
               		SUBSTRING_INDEX(
                   		SUBSTRING_INDEX(url, '?', 1), # split on url params to remove weirdest stuff first 
                   	'://', -1), # remove protocal http:// https:// ftp:// ...
				'/', 3), # split on path 
			'.', -2), # keep TLD + domain name
		'/', 1) AS domain
FROM ( 
    SELECT       'http://test.com' as url 
    UNION SELECT 'https://test.com' 
    UNION SELECT 'http://test.com/one' 
    UNION SELECT 'http://test.com/?huh' 
    UNION SELECT 'http://www.test1.test.com?http://ouch.foo' 
    UNION SELECT 'test.com' 
    UNION SELECT 'test.com/one'
    UNION SELECT 'test.com/one/two'
    UNION SELECT 'test.com/one/two/three'
    UNION SELECT 'test.com/one/two/three?u=http://maaaaannn'
    UNION SELECT 'http://one.test.com'
    UNION SELECT 'one.test.com/one'
    UNION SELECT 'two.one.test.com/one' ) AS test; 


# insert string (domain name) into field in same table  (single row)
UPDATE urls t1 
INNER JOIN (SELECT id, domain, url FROM urls t2 WHERE id = 1541) t2
ON t1.id = t2.id
SET t1.domain = (SELECT SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(t2.url, '/', 3), '://', -1), 'www.', -1), '/', 1), '?', 1));

# insert string (domain name) into field in same table  (all rows)
UPDATE urls t1 
INNER JOIN (SELECT id, domain, url FROM urls t2) t2
ON t1.id = t2.id
SET t1.domain = (SELECT SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(t2.url, '/', 3), '://', -1), 'www.', -1), '/', 1), '?', 1));
```
