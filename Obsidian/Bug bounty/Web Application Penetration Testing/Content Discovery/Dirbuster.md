---
tags:
  - Enumeration
  - Active-Recon
  - Brute-Force
  - Content-Discovery
---

# Overview
---

DirBuster is a tool designed for website directory and file enumeration. It can be used to discover hidden files and directories on a web server by brute-forcing common directory and file names. It is available as a standalone Java application and can be used on any platform that supports Java.

DirBuster is an essential tool for any penetration tester as it allows for the discovery of hidden web pages and directories that may be missed by normal web crawlers or search engines. The tool is particularly useful for testing the security of web applications by identifying potential areas of weakness that can be exploited by attackers.

# Options
---

- `-h` : Display this help message
- `-H` : Start DirBuster in headless mode (no gui), report will be auto saved on exit
- `-l` \<Word list to use> : The Word list to use for the list based brute force. Default: /home/kali/kali-www/bin/kali-tools/tool-output/dirbuster/directory-list-2.3-small.txt
- `-g` : Only use GET requests. Default Not Set
- `-e` \<File Extension list> : File Extension list eg asp,aspx. Default: php
- `-t` \<Number of Threads> : Number of connection threads to use. Default: 10
- `-s` \<Start point> : Start point of the scan. Default: /
- `-v` : Verbose output, Default: Not set
- `-P` : Don't Parse html, Default: Not Set
- `-R` : Don't be recursive, Default: Not Set
- `-r` \<location> : File to save report to. Default: /home/kali/kali-www/bin/kali-tools/tool-output/dirbuster/DirBuster-Report-[hostname]-[port].txt

# Examples

## Command line

- Basic directory brute-forcing
    
    ```bash
    dirb <http://example.com> -l /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
    ```
    
    > This command will start brute-forcing common directories and files on the `http://example.com` website using the `directory-list-2.3-medium.txt` wordlist.
    
- Headless mode with auto-saved report
    
    ```bash
    dirb <http://example.com> -H -r /path/to/report.txt -l /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
    ```
    
    > This command will launch DirBuster in headless mode, brute-force common directories and files on the `http://example.com` website using the `directory-list-2.3-medium.txt` wordlist, and auto-save the report to the specified location.
    
- Verbose output
    
    ```bash
    dirb <http://example.com> -v -l /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
    ```
    

## GUI

- Basic directory brute-forcing
    
    ```bash
    dirbuster -u <http://example.com> -l /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
    ```
    
    > This command will launch DirBuster in GUI mode and start brute-forcing common directories and files on the `http://example.com` website using the `directory-list-2.3-medium.txt` wordlist.
    
- Headless mode with auto-saved report
    
    ```bash
    dirbuster -u <http://example.com> -H -r /path/to/report.txt -l /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
    ```
    
    > This command will launch DirBuster in headless mode, brute-force common directories and files on the `http://example.com` website using the `directory-list-2.3-medium.txt` wordlist, and auto-save the report to the specified location.
    
- Brute-forcing with file extensions
    
    ```bash
    dirbuster -u <http://example.com> -l /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -e php,asp,aspx
    ```
    
    > This command will launch DirBuster in GUI mode and start brute-forcing common directories and files with the specified file extensions on the `http://example.com` website using the `directory-list-2.3-medium.txt` wordlist.
    
- Verbose output
    
    ```bash
    dirbuster -u <http://example.com> -v -l /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
    ```

