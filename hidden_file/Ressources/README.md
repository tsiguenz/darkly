# Hidden file

Scan the website with dirb and we get this:

```
 ==> DIRECTORY: http://192.168.64.3/admin/
 ==> DIRECTORY: http://192.168.64.3/whatever/
```

In /whatever we find a file containing this:

```
root:437394baff5aa33daa618be47b75cb49
```

Brute force the hash with john:

```
# john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt flag.txt
qwerty123@       (?)
```

Now go to /whatever and fill the form with the creds we get.
