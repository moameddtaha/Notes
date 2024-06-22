---
tags: 
Link:
  - "[[CORS]]"
---

## CORS Vulnerabilities
---

![[Pasted image 20240121034034.png]]
![[Pasted image 20240121034458.png]]
> [!NOTE] NOTE
> If you trust multiple origin, you're left with dynamically inspecting the origin header from the request and deciding if you trust it, if you trust it you reflected back to the user.
> 
> The portion in that process that introduces the security vulnerabilities or the security risks is the logic of the code that decides how you can determine if an origin is trusted by your application

![[Pasted image 20240121040356.png]]

***Whitelisted null origin value:***
- The specification for the Origin header supports the value `null`. Browsers might send the value `null` in the Origin header in various unusual situations:
	- Cross-origin redirects.
	- Requests from serialized data.
	- Request using the `file:` protocol.
	- Sandboxed cross-origin requests.

> [!NOTE] Server-generated header
> `Server-generated` `Access-Control-Allow-Origin` header is simply extracting the origin header from client side input and reflecting it back to the user so if we take my website run khalil.com as an example and my site is making a request to the shopping applications website what ends up happening is that when the shopping application sees my request all it does is it extracts the origin of my request which is renekalil.com and then it inserts it in the access control allow origin header thereby allowing my application to access its resources now this is equivalent to you using the wildcard character because it essentially will allow any origin that accesses it to access its resources all it's doing is extracting the origin and then reflecting it back to the user so there are obvious security issues with that because you're allowing all the origins on the internet to access your public resources.

> [!important] Null header
> The null header does not abide by the rules, you're allowed to send credentials using the null header and effectively if you decide to whitelist the null header any application on the internet can make it's request appear as if it's coming from the null origin and so that makes it much worse than the wildcard character.




