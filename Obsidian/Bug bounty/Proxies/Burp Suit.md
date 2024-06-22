---
tags:
  - Extensions
  - Proxy
---

# Extentions

## Bypass WAF

---

This extension add headers to all Burp requests to bypass some WAF products. The following headers are automatically added to all requests:

```
X-Originating-IP: 127.0.0.1
X-Forwarded-For: 127.0.0.1
X-Remote-IP: 127.0.0.1
X-Remote-Addr: 127.0.0.1
```

## **Logger++**

---

Logger++ is a multithreaded logging extension for Burp Suite. In addition to logging requests and responses from all Burp Suite tools, the extension allows advanced filters to be defined to highlight interesting entries or filter logs to only those which match the filter.

A built in grep tool allows the logs to be searched to locate entries which match a specified pattern, and extract the values of the capture groups.

To enable logs to be used in other systems, the table can also be uploaded to elasticsearch or exported to CSV. [Read More](https://portswigger.net/bappstore/470b7057b86f41c396a97903377f3d81)

## Hackvector

---

Hackvertor is a tag-based conversion tool that supports various escapes and encodings including HTML5 entities, hex, octal, unicode, url encoding etc.

- It uses XML-like tags to specify the type of encoding/conversion used.
- You can use multiple nested tags to perform conversions.
- Tags can also have arguments allowing them to behave like functions.
- It has an auto decode feature allowing it to guess the type of conversion required and automatically decode it multiple times.
- Multiple tabs
- Character set conversion

## Content Type Converter

---

This extension converts data submitted within requests between various common formats:

- JSON To XML
- XML to JSON
- Body parameters to JSON
- Body parameters to XML

This is useful for discovering vulnerabilities that can only be found by converting the content type of a request. For example, if an original request submits data using JSON, we can attempt to convert the data to XML, to see if the application accepts data in XML form. If so, we can then look for vulnerabilities like XXE injection which would not arise in the context of the original JSON endpoint. It might also be possible to find vulnerabilities behind web application firewalls or other filters that assume the incoming data is in a specific format, while the application tolerates data in other formats.

Requires Java version 8.

## **DOM Invader**

---

DOM Invader is a browser-based tool that helps you test for [DOM XSS](https://portswigger.net/web-security/cross-site-scripting/dom-based) vulnerabilities using a variety of sources and sinks, including both web message and [prototype pollution](https://portswigger.net/web-security/prototype-pollution) vectors. It is available exclusively via Burp's built-in browser, where it comes preinstalled as an extension.

![[a.png]]

[DOM Invader](https://portswigger.net/burp/documentation/desktop/tools/dom-invader)


## Upload Scanner
---
Testing web applications is a standard task for every security analyst. Various automated and semi-automated security testing tools exist to simplify the task. HTTP based file uploads are one specialised use case. However, most automated web application security scanners are not adapting their attacks when encountering file uploads and are therefore likely to miss vulnerabilities related to file upload functionalities.

You can read more here [Upload Scanner](https://portswigger.net/bappstore/b2244cbb6953442cb3c82fa0a0d908fa)


## Decoder Improved
---
Decoder Improved is a data transformation plugin for Burp Suite that better serves the varying and expanding needs of information security professionals.

You can read more here [Decoder Improved](https://portswigger.net/bappstore/0a05afd37da44adca514acef1cdde3b9)


## Some extensions worth checking out include, but are not limited to:
---

| Tool                          | Tool                           | Tool                          |
|-------------------------------|--------------------------------|------------------------------|
| .NET beautifier               | J2EEscan                       | Software Vulnerability Scanner|
| Software Version Reporter     | Active Scan++                  | Additional Scanner Checks    |
| AWS Security Checks           | Backslash Powered Scanner      | Wsdler                       |
| Java Deserialization Scanner  | C02                            | Cloud Storage Tester         |
| CMS Scanner                   | Error Message Checks           | Detect Dynamic JS            |
| Headers Analyzer              | HTML5 Auditor                  | PHP Object Injection Check   |
| JavaScript Security           | Retire.JS                      | CSP Auditor                  |
| Random IP Address Header      | Autorize                       | CSRF Scanner                 |
| JS Link Finder                |                                |                              |

















