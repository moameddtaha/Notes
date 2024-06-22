---
tags: 
Link:
  - "[[CSRF]]"
---

## Black-Box Testing Perspective
---
1. Map the application
	- Review all the key functionality in the application
2. Identify all application functions that satisfy the following three conditions
	- A relevant action (that cause a tremendous effect).
	- Cookie-based session handling.
	- NO unpredictable request parameters.
3. Create a PoC script to exploit CSRF
## White-Box Testing Perspective
---
1. Identify the framework that is being used by the application.
2. Find out how this framework defends against CSRF attacks.
3. Review code to ensure that the built in defenses have not been disabled.
3. Review all the sensitive functionality to ensure that the CSRF defense has been applied.