# Cookie_forgery

### Breach Exploit

In the cookies we can see this:

|Name      |Value                           |
|----------|--------------------------------|
|I_am_admin|b326b5062b2f0e69046810717534cb09|

We found with dcode the value of the cookie means false in md5 and we do md5(true) to get the new value.

```
md5(true) = b326b5062b2f0e69046810717534cb09
```

After change the value, we get the flag in an alert.

### Fix Breach

Do not store sensitive data in cookie, and do not use md5 
```https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html```

### Documentation
```https://owasp.org/www-community/attacks/csrf```
