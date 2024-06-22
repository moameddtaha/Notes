---
tags:
  - Database-Management-System
---

# MySQL

---

MySQL is an open-source relational database management system based on SQL (Structured Query Language).

It is typically used to store records, customer data, and is most commonly deployed to store web application data.

MySQL utilizes TCP port 3306 by default, however, like any service it can be hosted on any open TCP port.

We can utilize auxiliary modules to enumerate the version of MySQL, perform brute-force attacks to identify passwords, execute SQL queries and much more.

## Commands

---

- Connect to remote MySQL database
    
    ```sql
    mysql -h <IP> -u <USER> -p
    ```
    
    > Remove `-p` if you want to connect without a password.
    
- Show permissions
    
    ```sql
    SHOW GRANTS;
    ```
    
- Show databases
    
    ```sql
    SHOW DATABASES;
    ```
    
- Select database
    
    ```sql
    USE <database_name>;
    ```
    
- Show tables
    
    ```sql
    SHOW TABLES;
    ```
    
- Select columns from table
    
    ```sql
    SELECT * FROM <table_name>;
    ```
    
- How many records are present in table
    
    ```sql
    select count(*) from <table>;
    ```
    
- Find the system password hash for user.
    
    ```sql
    select load_file("/etc/shadow")
    ```
    
- Format the output in user friendly
    
    ```sql
    SELECT * FROM user\\\\G
    ```
    
    This will display the output vertically, which can make it easier to read. The `\\\\G` option is used to format the output in a more readable way.
    





