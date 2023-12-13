
## Strings

#### References

* [SUBSTRING_INDEX](https://www.w3schools.com/sql/func_mysql_substring_index.asp)



```sql

# basic substring examples
SELECT SUBSTRING_INDEX('hello world!',' ', 1); # hello
SELECT SUBSTRING_INDEX('http://www.test.com/path/','://', -1); # www.test.com/path/ 


# get the domain name from url (impossible to remove subdomains without removing *.co.uk type domains)
SELECT SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(url, 
'?', 1), # split on url params to remove weirdest stuff first 
'://', -1), # remove protocal http:// https:// ftp:// ...
'/', 1), # split on path 
':', 2), # split on user:pass
'@', 1), # split on user:port@
':', 1), # split on port
'www.', -1), # remove www.
'.', 4), # keep TLD + domain name
'/', 1) 
AS domain
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
    UNION SELECT 'https://www.bbc.co.uk/'
    UNION SELECT 'http://a.very.complex-domain.co.uk:8080/foo/bar'
    UNION SELECT 'postgres://user:pass@host.com:5432/path?k=v#f'
    UNION SELECT 'http://10.64.3.5/data_check/index.php?r=index/rawdatacheck'
    UNION SELECT 'two.one.test.com/one' ) AS test; 



# insert string (domain name) into field in same table  (single row)
UPDATE urls t1 
INNER JOIN (SELECT id, domain, url FROM urls t2 WHERE id = 1541) t2
ON t1.id = t2.id
SET t1.domain = (SELECT SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(t2.url, 
'?', 1), # split on url params to remove weirdest stuff first 
'://', -1), # remove protocal http:// https:// ftp:// ...
'/', 1), # split on path 
':', 2), # split on user:pass
'@', 1), # split on user:port@
':', 1), # split on port
'www.', -1), # remove www.
'.', 4), # keep TLD + domain name
'/', 1) 
);

# insert string (domain name) into field in same table  (all rows)
UPDATE urls t1 
INNER JOIN (SELECT id, domain, url FROM urls t2) t2
ON t1.id = t2.id
SET t1.domain = (SELECT SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(SUBSTRING_INDEX(t2.url, 
'?', 1), # split on url params to remove weirdest stuff first 
'://', -1), # remove protocal http:// https:// ftp:// ...
'/', 1), # split on path 
':', 2), # split on user:pass
'@', 1), # split on user:port@
':', 1), # split on port
'www.', -1), # remove www.
'.', 4), # keep TLD + domain name
'/', 1) 
);


```



### Create slug using existing column

```mysql

UPDATE defense_items SET
    slug = lower(title),
    slug = replace(slug, '.', ' '),
    slug = replace(slug, ',', ' '),
    slug = replace(slug, ';', ' '),
    slug = replace(slug, ':', ' '),
    slug = replace(slug, '"', ' '),
    slug = replace(slug, '?', ' '),
    slug = replace(slug, '%', ' '),
    slug = replace(slug, '$', ' '),
    slug = replace(slug, '&', ' '),
    slug = replace(slug, '#', ' '),
    slug = replace(slug, '*', ' '),
    slug = replace(slug, '!', ' '),
    slug = replace(slug, '_', ' '),
    slug = replace(slug, '@', ' '),
    slug = replace(slug, '+', ' '),
    slug = replace(slug, '(', ' '),
    slug = replace(slug, ')', ' '),
    slug = replace(slug, '[', ' '),
    slug = replace(slug, ']', ' '),
    slug = replace(slug, '/', ' '),
    slug = replace(slug, '-', ' '),
    slug = replace(slug, '\'', ''),
    slug = trim(slug),
    slug = replace(slug, ' ', '-'),
    slug = replace(slug, '--', '-'),
    slug=replace(slug, 'ä', 'a'),
    slug=replace(slug, 'å', 'a'),
    slug=replace(slug, 'æ', 'a'),
    slug=replace(slug, 'ç', 'c'),
    slug=replace(slug, 'è', 'e'),
    slug=replace(slug, 'é', 'e'),
    slug=replace(slug, 'ê', 'e'),
    slug=replace(slug, 'ë', 'e'),
    slug=replace(slug, 'ì', 'i'),
    slug=replace(slug, 'í', 'i'),
    slug=replace(slug, 'î', 'i'),
    slug=replace(slug, 'ï', 'i'),
    slug=replace(slug, 'ð', 'o'),
    slug=replace(slug, 'ñ', 'n'),
    slug=replace(slug, 'ò', 'o'),
    slug=replace(slug, 'ó', 'o'),
    slug=replace(slug, 'ô', 'o'),
    slug=replace(slug, 'õ', 'o'),
    slug=replace(slug, 'ö', 'o'),
    slug=replace(slug, 'ø', 'o'),
    slug = replace(slug, 'ù','u'),
    slug = replace(slug, 'ú','u'),
    slug = replace(slug, 'û','u'),
    slug = replace(slug, 'ü','u'),
    slug = replace(slug, 'ý','y'),
    slug = replace(slug, 'ë','e'),
    slug = replace(slug, 'à','a'),
    slug = replace(slug, 'á','a'),
    slug = replace(slug, 'â','a'),
    slug = replace(slug, 'ã','a'),
    slug= replace(slug, '%', ''),
    slug= replace(slug, 'ç', 'c'),
    slug= replace(slug, 'ü', 'u'),
    slug= replace(slug, 'ğ', 'g'),
    slug= replace(slug, 'ş', 's'),
    slug= replace(slug, 'ß', 'b'),
    slug= replace(slug, 'ı', 'i'),
    slug= replace(slug, '.', ''),
    slug= replace(slug, 'ö', 'ö'),
    slug= replace(slug, 'ç', 'c'),
    slug= replace(slug, '#x27;', ''),
    slug = replace(slug, '--', '-');

# And then test the results with:

SELECT * FROM defense_items WHERE
    slug NOT RLIKE '^([a-z0-9]+\-)*[a-z0-9]+$';

```





### Finding and replacing strings


```mysql


# REPLACE CHARACTES

# tests - search for/replace "é"
SELECT * FROM defense_items WHERE text LIKE "%Ã©%";
SELECT REPLACE('resumÃ©s in hand', "Ã©","é") LIMIT 1;

# replace in table
UPDATE defense_items SET text = REPLACE(text, "Ã©","é");
UPDATE defense_items SET text = REPLACE(text, "â€œ",'"'); # left curly
UPDATE defense_items SET text = REPLACE(text, "â€",'"'); # right curly
UPDATE defense_items SET text = REPLACE(text, "â€¢",'-');





# test - concatenate a string to another randomly selected string

SELECT CONCAT("assets/img/avatars/", elt(floor(rand()*3) + 1, 
	"avatar-generic-zigzag-mad.png",
	"avatar-generic-yellow-blush.png",
	"avatar-generic-rainbow-up.png"
));


# update users, concatenate a string to another randomly selected string

UPDATE
    users
SET
    avatarPath = CONCAT("assets/img/avatars/", elt(floor(rand()*16) + 1, 
        "avatar-cyan-sad.png",
        "avatar-grad-glasses-sun-green.png",
        "avatar-grad-glasses-tape.png",
        "avatar-grad-pirate.png",
        "avatar-grad-rainbow-sad.png",
        "avatar-grad-rainbow-up.png",
        "avatar-magenta.png",
        "avatar-orange-glasses-sun-sunset.png",
        "avatar-pattern-glasses-sun-60s.png",
        "avatar-pattern-pink-glasses-sun-future.png",
        "avatar-pattern-plaid-glasses-groucho.png",
        "avatar-pattern-plaid-glasses-sun-roadie.png",
        "avatar-pattern-plaid-sad.png",
        "avatar-pattern-zigzag-mad.png",
        "avatar-yellow-blush.png",
        "avatar-yellow-wing-glasses.png"
)) 
WHERE avatarPath IS NULL OR avatarPath LIKE "%/avatar-%";

```




