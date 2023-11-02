# XSS_STORED

### Breach Exploit

In the page ```/index.php?page=feedback``` we can create a new feedback by filling out the form.
There is an error in form validation:

```javascript
function validate_required(field,alerttxt)
{
with (field) {
  if (value==null||value=="") {
    alert(alerttxt);return false;
  }
  else {
    return true;
  }
 }
}

function validate_form(thisform) {
with (thisform) {

  if (validate_required(txtName,"Name can not be empty.")==false)
  {txtName.focus();return false;}
  
  if (validate_required(mtxMessage,"Message can not be empty.")==false)
  {mtxMessage.focus();return false;}
  
  }
}
```

In this code we can see the validation fields are named txtName and mtxMessage but they name in the html part are:

```html
<td> <input name="txtName" type="text" size="30" maxlength="10"> </td>
<td> <textarea name="mtxtMessage" cols="50" rows="3" maxlength="50"></textarea> </td>
```

We can see that the field mtxMessage is not the same as mtxtMessage.

So we can fill the form with a valid value for the Name and bad value for the Message like 'a' and nothing and we get the flag.

### Fix Breach
Never trust user input, always sanitize input
```https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html```

### Documentation
```https://cheatsheetseries.owasp.org/cheatsheets/XSS_Filter_Evasion_Cheat_Sheet.html```
