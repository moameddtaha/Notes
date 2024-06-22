---
tags: 
Link:
  - "[[CORS]]"
---

# Black-Box Testing
---

- Map the application
- Test the application for dynamic generation
	- Does it reflect the user-supplied ACAO header?
	- Does it only validate on the start/end of a specific string?
	- Does it allow the null origin?
	- Does it restrict the protocol?
	- Does it allow credentials?
- Once you have determined that CORS vulnerability exists, review the application's functionality to determine how you can prove impact.

# White-Box Testing
---

- Identify the framework/technologies that is being used by the application.
- Find out how this specific technology allows for CORS configuration.
- Review code to identify any misconfigurations in CORS rules.


























