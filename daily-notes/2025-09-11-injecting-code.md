# Injecting Code

## Into Interrupted Language
Attackers' input gets passed directly to the interpreter and runs as if it’s legit code.  

- depends upon the language targeted  
- programming technique employed by the application developer  
- supplying unexpected syntax may cause read errors → check for indication of code injection vulnerability  

## Injecting Into SQL
- databases are used by almost all web applications to store data like user details, prices, account statements, etc.  
- by editing certain commands or statements and using vulnerable web parts, we can read, update, add, and delete data in the database  

## Bypassing a Login
Every login page is connected to the backend most of the time, where it checks for username and password, and if they match, it lets you log in.  

- but we can bypass this login check if we know a username  
- example:  

```
SELECT * FROM USERS WHERE USERNAME ='ADMIN'--' AND PASSWORD='FOO'
```

This is equivalent to:  

```
SELECT * FROM USERS WHERE USERNAME ='ADMIN'
```

=> this way, the password check has been bypassed altogether  

- if you don’t know a username, you can use:  

```
USERNAME =' OR 1=1--
```

- this is always true, so it can help bypass some commands  
```
