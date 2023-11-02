# Server Side Request Forgery

### Breach Exploit
In the footer we can find links who redirect to Facebook, Twitter (X) and Instagram.

Have a look to the html:

```html
<li><a href="index.php?page=redirect&amp;site=facebook" class="icon fa-facebook"></a></li>
```

We can see the "site" parameter is facebook. Try to change it by something.

```
/?page=redirect&site=asdf
```

We get the flag!

### Fix Breach

Do not accept redirection using client input

```https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html```

### Documentation
```https://owasp.org/Top10/A10_2021-Server-Side_Request_Forgery_%28SSRF%29/```