# Content-Type bypass

### Breach Exploit

In the page '/?page=upload#' we can upload an image but not every extension.
For exemple jpeg and jpg are working but when we try to upload png image we get this "Your image was not uploaded.".

To get the flag I just change try to upload a png image and change the content type of the request by jpeg.


### Fix Breach
-Validate the file type, don't trust the Content-Type header as it can be spoofed
-Check and block not accepted files types
-Check and limit accepted filesize

```https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html```

### Documentation
```https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload```