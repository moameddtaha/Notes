---
tags:
  - Cheatsheet
---

[Sql Injection Cheatsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)


> [!NOTE] Note
> - The reason for using `NULL` as the values returned from the injected `SELECT` query is that the data types in each column must be compatible between the original and the injected queries. Since `NULL` is convertible to every commonly used data type, using `NULL` maximizes the chance that the payload will succeed when the column count is correct.
> - On Oracle, every `SELECT` query must use the `FROM` keyword and specify a valid table. There is a built-in table on Oracle called `dual` which can be used for this purpose. So the injected queries on Oracle would need to look like:
>   `' UNION SELECT NULL FROM DUAL--`
> - The payloads described use the double-dash comment sequence `-` to comment out the remainder of the original query following the injection point. On MySQL, the double-dash sequence must be followed by a space. Alternatively, the hash character `#` can be used to identify a comment. 
