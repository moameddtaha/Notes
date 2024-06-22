---
tags:
  - Networking
  - HTTP
  - APIs
  - Command-Line
  - Web-Development
  - Data-Transfer
  - Security
  - HTTPS
---

# cURL
---

[cURL](https://curl.haxx.se/) (client URL) is a command-line tool and library that primarily supports HTTP along with many other protocols. This makes it a good candidate for scripts as well as automation, making it essential for sending various types of web requests from the command line, which is necessary for many types of web penetration tests.

## Cheat Sheet
---

### cURL
---

| **Options**                                                                                                      | **Description**                                      |
| ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| `curl -h`                                                                                                        | cURL help menu                                       |
| `curl inlanefreight.com`                                                                                         | Basic GET request                                    |
| `curl -s -O inlanefreight.com/index.html`                                                                        | Download file                                        |
| `curl -k https://inlanefreight.com`                                                                              | Skip HTTPS (SSL) certificate validation              |
| `curl inlanefreight.com -v`                                                                                      | Print full HTTP request/response details             |
| `curl -I https://www.inlanefreight.com`                                                                          | Send HEAD request (only prints response headers)     |
| `curl -i https://www.inlanefreight.com`                                                                          | Print response headers and response body             |
| `curl https://www.inlanefreight.com -A 'Mozilla/5.0'`                                                            | Set User-Agent header                                |
| `curl -u admin:admin http://<SERVER_IP>:<PORT>/`                                                                 | Set HTTP basic authorization credentials             |
| `curl http://admin:admin@<SERVER_IP>:<PORT>/`                                                                    | Pass HTTP basic authorization credentials in the URL |
| `curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:<PORT>/`                                     | Set request header                                   |
| `curl 'http://<SERVER_IP>:<PORT>/search.php?search=le'`                                                          | Pass GET parameters                                  |
| `curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/`                                     | Send POST request with POST data                     |
| `curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/`                                      | Set request cookies                                  |
| `curl -X POST -d '{"search":"london"}' -H 'Content-Type: application/json' http://<SERVER_IP>:<PORT>/search.php` | Send POST request with JSON data                     |

> [!tip] tip
> The `-vvv` flag shows an even more verbose output.

> [!info] info
> Some headers, like the `User-Agent` or `Cookie` headers, have their own flags. For example, we can use the `-A` to set our `User-Agent`, as follows: (Please ignore the `\` character in front of any `>` or `<` character)
> ```shell-session
> P4ND4S4mur4i@htb[/htb]$ curl https://www.inlanefreight.com -A 'Mozilla/5.0'
> <!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
> \<html>\<head>
> ..SNIP...
> ```

> [!tip] tip
> There is another method we can provide the `basic HTTP auth` credentials, which is directly through the URL as (`username:password@URL`), as we discussed in the first section. If we try the same with cURL or our browser, we do get access to the page as well

### APIs
---

| **Command**                                                                                                                                             | **Description**       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| `curl http://<SERVER_IP>:<PORT>/api.php/city/london`                                                                                                    | Read entry            |
| `curl -s http://<SERVER_IP>:<PORT>/api.php/city/ \| jq`                                                                                                 | Read all entries      |
| `curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'`          | Create (add) entry    |
| `curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'` | Update (modify) entry |
| `curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City`                                                                                    | Delete entry          |

> [!NOTE] NOTE
> The HTTP `PATCH` method may also be used to update API entries instead of `PUT`. To be precise, `PATCH` is used to partially update an entry (only modify some of its data "e.g. only city_name"), while `PUT` is used to update the entire entry. We may also use the HTTP `OPTIONS` method to see which of the two is accepted by the server, and then use the appropriate method accordingly.

> [!NOTE] NOTE
> In some APIs, the `Update` operation may be used to create new entries as well. Basically, we would send our data, and if it does not exist, it would create it. For example, in the above example, even if an entry with a `london` city did not exist, it would create a new entry with the details we passed. In our example, however, this is not the case.




























