---
tags:
  - Enumeration
  - Active-Recon
  - Brute-Force
  - Content-Discovery
---

# About
---

Gobuster is a powerful tool used for brute-forcing URIs, DNS subdomains, virtual hosts, and various other targets. It's particularly useful for web application penetration testing and vulnerability assessments.

Gobuster is a tool used to brute-force:

- URIs (directories and files) in web sites.
- DNS subdomains (with wildcard support).
- Virtual Host names on target web servers.
- Open Amazon S3 buckets
- Open Google Cloud buckets
- TFTP servers

# Options
---

Gobuster has several options that can be used to customize and fine-tune the scanning process. Some of the most commonly used options include:

- `u`: specifies the target URL to be scanned.
- `w`: specifies the wordlist to be used for the brute-force attack.
- `t`: specifies the number of threads to be used for the scan.
- `k`: skips SSL certificate verification.
- `x`: specifies the file extensions to be checked for in the directories.
- `s`: specifies the status codes to be considered valid during the scan.
- `e`: specifies the user-agent string to be used in HTTP requests.
- `vhost`: Specifies a virtual host (VHOST) to use for subdomain enumeration.

# Examples
---

Here are some examples of how Gobuster can be used:

1. To scan a website for directories and files, use the following command:
    
    ```bash
    gobuster dir -u <https://example.com> -w wordlist.txt
    ```
    
     This command tells Gobuster to scan the website at `https://example.com` using the wordlist `wordlist.txt`.
    

- To scan a website for directories and files with a specified file extension, use the following command:
    
    ```bash
    gobuster dir -u <https://example.com> -w wordlist.txt -x php
    ```
    
     This command tells Gobuster to scan the website at `https://example.com` using the wordlist `wordlist.txt`, and only look for files with the `.php` extension.
    
- To scan a website for subdomains, use the following command:
    
    ```bash
    gobuster dns -d example.com -w wordlist.txt
    ```
    
    This command tells Gobuster to scan for subdomains of the `example.com` domain using the wordlist `wordlist.txt`.

> [!NOTE] 💡Note 
>  By default, GoBuster uses the `A`, `AAAA`, `CNAME`, and `TXT` record types to enumerate subdomains. You can use the `-t` option to specify a different record type, or you can use the `-t ALL` option **to use all available record types.**

> [!NOTE] 💡 Note
> The `gobuster dns` command is useful for discovering subdomains of a particular domain or VHOST that may not be listed in public DNS records. It can be used as part of a broader enumeration or reconnaissance effort to identify potential targets for further analysis or attack.

    
- You can also use the `vhost` option to specify a virtual host (VHOST) to use for the subdomain enumeration. This can be useful if the web server uses VHOSTs to host multiple websites on a single IP address. For example:
    
    ```bash
    gobuster vhost -u <URL> -w <common-vhosts.txt>
    ```
    
     This would tell GoBuster to enumerate subdomains for the [example.com](http://example.com) VHOST using the wordlist specified in the wordlist.txt file.


