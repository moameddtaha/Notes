---
tags:
  - Client-Side
External Link:
  - https://portswigger.net/web-security/cors
  - https://www.youtube.com/watch?v=t5FBwq-kudw
  - https://portswigger.net/web-security/cors/access-control-allow-origin
---

# CORS
---

![[Pasted image 20240120062107.png]]
![[Pasted image 20240120064442.png]]

## How the server and browser behave once CORS rules are configured
---

### CORS Configuration
---
![[Pasted image 20240120064549.png]]

### CORS Headers
---
![[Pasted image 20240120064929.png]]

#### Access-Control-Allow-Origin Header
---

> [!NOTE] NOTE
> ==The `Access-Control-Allow-Origin` header allows you to only access public pages in the application==. In order to access authenticated pages you need to use another header called the [[CORS#Access-Control-Allow-Credentials Header|Access-Control-Allow-Credentials Header]] Access-Control-Allow-Credentials Header.

![[Pasted image 20240120065154.png]]

> [!NOTE] NOTE
> ==`Acess-Control-Allow-Origin` only allow whitelist single origin== not multiple origin. This contributes to the issue of people trying to get around that and this contributes to why there are so many security issues because most sites need to trust multiple domains however that's not an option.

![[Pasted image 20240120065351.png]]

#### Access-Control-Allow-Credentials Header
---

![[Pasted image 20240120070508.png]]
![[Pasted image 20240120070657.png]]

> [!NOTE] NOTE
> ==If the server is configures with the wildcard ("`*`") as the value of `Access-Control-Allow-Origin` header, then the use if credentials is not allowed.== The reason is for security purposes, if you got the `Access-Control-Allow-Origin` header set to start that means any origin on the internet is allowed to access the website and if the specification had allowed this type of configuration to be set with `Access-Control-Allow-Credentials` header to set to true that means not only can any origin or domain on the internet access your recourses it can also access you authenticated recourses and this causes a huge problem.






















































