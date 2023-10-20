# RECOVER

When we click on forget password we get this page ```/?page=recover#```

In this page we can click on submit button but Wrong Answer appear.

Lets see the request send by 'submit':

```
POST http:{IP}/?page=recover#
Body: mail=webmaster.com&Submit=Submit
```

In the source code we can find this:

```html
<input type="hidden" name="mail" value="webmaster@borntosec.com" maxlength="15">
```

- Change the value of this field by 'exploit' for exemple and we get the flag when we click on submit.

- We can change the value of the body in the request to get the flag.
