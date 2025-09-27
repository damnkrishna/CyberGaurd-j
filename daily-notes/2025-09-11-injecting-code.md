# Injecting Code

## Into Interpreted Language
Attackers' input gets passed directly to the interpreter and runs as if it’s legit code.  
- Depends upon the language targeted.  
- Programming technique employed by the application developer.  
- Supplying unexpected syntax may cause read errors → check for indication of code injection vulnerability.  

## Injecting Into SQL
- Databases are used by almost all web applications to store data like user details, prices, account statements, etc.  
- By editing certain commands or statements and using vulnerable web parts, we can read, update, add, and delete data in the database.  

## Retrieving Hidden Data
Check if SQL injection is possible or not:  
- Try single quotation or double quotation as input.  
- Try `--` → observe the response.  
- Try `%` → if the server is interacting with the back-end database, submitting `%` may return some table or data.  
- Try `' OR 1=1--` → will bypass any true statement check, as `1=1` is always true.  
- Try supplying a mathematical expression that is equivalent to the original numerical value.  

**Useful notes:**  
- Use ASCII commands and quotes.  
- Remember:  
  - spaces ⇔ `+` or `%20`  
  - `+` ⇔ `%2b`  
  - `;` ⇔ `%3b`  

## Bypassing a Login
Every login page is connected to the backend most of the time, where it checks for username and password. If they match, it lets you log in.  

- We can bypass this login check if we know a username.  
- Example:  
```
SELECT * FROM USERS WHERE USERNAME = 'ADMIN'--' AND PASSWORD = 'FOO'
```
This is equivalent to:  
```
SELECT * FROM USERS WHERE USERNAME = 'ADMIN'
```
⇒ This way, the password check has been bypassed altogether.  

- If you don’t know a username, you can use:  
```
USERNAME = ' OR 1=1--
```
- Since `1=1` is always true, this can bypass the check.  

## Subverting Application Logic
- Example: username = `wiener` and password = `bluecheese`.  
- This can be bypassed using:  
  - If you have a username like `administrator`, try:  
    ```
    administrator'--
    ```
  - If you don’t have a username, then try:  
    ```
    username = admin
    password = ' OR 1=1--
    ```  

## Injecting into Different Statement Types
The most common types of SQL statements are:  

- **SELECT**  
- **INSERT**  
  - Use this for finding table column size and type, e.g.:  
    ```
    foo')--
    foo',1)--
    foo',1,1)--
    ```  
- **UPDATE**  
  - Example of bypassing password check and resetting the password:  
    ```
    update users set password='newsecret' where user='admin' or 1=1
    ```  
- **DELETE**  
- **The UNION operator**  
- **Fingerprinting the database**  
- **Extracting useful data**  

**Notes:**  
- If you don’t know the data type of columns in a table, you can always use:  
  ```
  SELECT NULL
  ```
- Use trial-and-error to find table names, column types, and column names.  

### Techniques
- If the `SELECT` statement is blocked or removed, try:  
  ```
  SeLeCt
  SELSELECTECT
  %53%54%4C%45%43%54
  ```
- In MySQL, comments can be inserted within keywords to bypass validation, for example:  
  ```
  SEL /*FOO*/ECT username,password FR/*foo*/OM users
  ```
- If the defense filter escapes or doubles up a single quotation mark, you can bypass it with escape quotations. Example:  
  ```
  aaaa'
  ```

## Second Order SQL Injection
- An attacker can register a username containing crafted input and then attempt to change their password.  
- Example:  
  ```
  'or 1 in (select password from users where username='admin')--
  ```
- When the attacker tries to change their password, the injected query will be executed → Revealing the admin password.  

**Note:** Not every attack is about stealing information — some just want to destroy your system/device.

