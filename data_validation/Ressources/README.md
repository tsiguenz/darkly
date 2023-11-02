# Access Control

### Breach Exploit
In url: "/?page=survey#" we can see a survey (surprising ?).

We can vote for someone and inspect the body of the POST request:

```
sujet=2&valeur=5
```

Change the value of sujet and nothing append.

Change the value of valeur to 100 for example and we have the flag in response.

### Fix Breach
Always implement input data validation on the backend, in this case only a 'valeur' between 1 and 10 should be accepted
```https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html```

### Documentation
```https://owasp.org/www-community/vulnerabilities/Improper_Data_Validation```
