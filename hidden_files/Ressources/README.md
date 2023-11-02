# Hidden files

### Breach Exploit
With gobuster we find the file robots.txt who list some path forbidden for the crawlers:

```bash
$ gobuster dir -w `fzf-wordlists` -u http://192.168.56.101/ --exclude-length=975
...
/robots.txt           (Status: 200) [Size: 53]
...
```

/robots.txt:

```
User-agent: *
Disallow: /whatever
Disallow: /.hidden
```

When we go to /.hidden we can see a lots of directories with README in each of them.
We hope the flag is in a README so we download all the readme to grep something in the folders:

```bash
$ wget -r -np -nH -e robots=off -A README http://192.168.56.101/.hidden/
...
$ grep -R "flag" .hidden
.hidden/.../README:Hey, here is your flag : d5eec3ec36cf80dce44a896f961c1831a05526ec215693c8f2c39543497d4466
```
### Fix Breach
Do not store sensitive information on the client side

### Documentation
```https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/01-Information_Gathering/03-Review_Webserver_Metafiles_for_Information_Leakage```