---
tags:
  - Database-Management-System
  - Metasploit
  - Nmap
---


> [!NOTE] 📢 Note
> Default port 1433

# Nmap

---

- Prefered to go to Nmap website and search for scripts.
    
    [Nmap: the Network Mapper - Free Security Scanner](https://nmap.org/)
    

# Metasploit

---

<aside> 💡 Prefer to go search in metasploit framework.

</aside>

- Identifying valid MSSQL users and their passwords using provided username and password list using metasploit module mssql_login.

    ```bash
    use auxiliary/scanner/mssql/mssql_login
    ```
    
    set USER_FILE /root/Desktop/wordlist/common_users.txt set PASS_FILE /root/Desktop/wordlist/100-common-passwords.txt

- Running MSSQL enumeration module to find all possible information.
    
    ```bash
    use auxiliary/admin/mssql/mssql_enum
    ```
    
- Extract all MSSQL users
    
    ```bash
    use auxiliary/admin/mssql/mssql_enum_sql_logins
    ```
    
- Execute a command using mssql_exec module.
    
    ```bash
    use auxiliary/admin/mssql/mssql_exec
    ```
    
- Running MSSQL enum domain accounts module. This module dumps the information such as Windows domain users, groups, and computer accounts.
    
    ```bash
    use auxiliary/admin/mssql/mssql_enum_domain_accounts
    ```




