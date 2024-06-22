---
tags: 
Link:
  - "[[CSRF]]"
External Link:
  - https://portswigger.net/web-security/csrf/preventing
---

# Preventing CSRF Variabilities
---
## Primary Defense
---
 - Use a CSRF token in relevant requests.
	 - **How should CSRF tokens be generated?**
		 - Unpredictable with high entropy, similar to session tokens.
		 - Tied to the user's session
		 - Validated before the relevant action is executed
	 - **How should CSRF tokens be transmitted?**
		 1. Hidden filed of an html form that is submitted using a POST method
		 2. Custom request header - not very common
		 3. Tokens submitted in the URL query string are less secure
		 4. Tokens generally should not be transmitted within cookies - less secure
	- **How should CSRF tokens be validated?**
		1. Generated tokens should be stored server-side within the user's session data.
		2. When performing a request, a validation should be performed that verifies that the submitted token matches the value that is stored in the user's session.
		3. Validation should be performed regardless of HTTP method or content type of the request.
		4. If a token is not submitted, the request should be rejected.
 
## Additional Defense
---
- Use of [[Same-Site cookie]]
	- The same attribute can be used to control whether cookies are submitted in cross-site requests. 
		1. `Set-Cookie: session=0F8tgdOhi9ynR1M9wa3ODa; SameSite=Strict`
		2. `Set-Cookie: session=0F8tgdOhi9ynR1M9wa3ODa; SameSite=Lax`
		3. `Set-Cookie: session=0F8tgdOhi9ynR1M9wa3ODa; SameSite=None; Secure`
## Inadequate Defense
---
- Use of [Referrer header](https://portswigger.net/web-security/csrf/bypassing-referer-based-defenses) 
	**The Referrer HTTP request header contains an absolute or partial address of the page making the request.**
	- Referrer header can be spoofed
	- The defense can usually be bypassed:
		1. Example #1 - if it's not present, the application does not check for it.
		2. Example #2 - the referrer header is only checked to see if it contains the domain and exact match is not made.

