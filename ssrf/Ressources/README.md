# Server Side Request Forgery

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
